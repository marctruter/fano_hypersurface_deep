# Terminal Fano 4-fold Hypersurfaces via Deep Reinforcement Learning

**Source code and data for [*Terminal Fano 4-fold Hypersurfaces via Deep Reinforcement Learning*](https://arxiv.org/abs/2603.15437).**

We study the discovery of terminal Fano fourfold hypersurfaces of index one,

$$
X_d\subset\mathbb{P}(a_1,\ldots,a_6),\qquad d=\sum_{i=1}^{6}a_i-1,
$$

using best-first searches over the integer lattice of weights. We compare a **fixed heuristic** with a **dynamic heuristic** learned online through deep reinforcement learning, and use an **ablation search** to distinguish learning from stochastic exploration alone.

## Main results

- **46,992** previously unknown nonquasismooth terminal families with equation degree $d>200$.
- **121,980** distinct nonquasismooth terminal families across all degrees, combining the heuristic searches.
- Discovered families with equation degrees up to **3,234**.
- The fixed heuristic finds more families overall, whereas the dynamic heuristic explores more isolated regions of weight space, discovering an average of **79 ± 9** hard-to-reach families per run across five runs.

The paper describes the search algorithms, terminality certification, distance analysis and ablation experiments. The consolidated classification is [archived on Zenodo](https://doi.org/10.5281/zenodo.23837634) [4].

## Repository structure

```text
code/                                  Search and analysis scripts/notebooks

data/
  quasismooth/
    quasismooth_terminal.csv           Reference quasismooth classification
  fixed/                                Fixed-search results and certification data
  dynamic/                              Dynamic-search results and certification data
  ablation/                             Ablation-search results
  union/
    union_certification/
      union_certification_short.csv    Unique weight vectors (no header)
      union_certification_short.pkl    Degree and weight records
      union_certification_medium.pkl   Condensed singularity records
      union_certification_long.pkl     Detailed certification records
      union_certification_raw.pkl      Raw records and certification outcomes

figures/                                Figures generated for the paper
LICENSE                                 MIT license
README.md
```

## Classification and certification data

### Combined heuristic-search datasets

The files in [`data/union/union_certification/`](data/union/union_certification/) combine the fixed search and all five dynamic runs. Processed datasets contain distinct certified terminal families, identified by their weight vectors. The raw dataset retains certification outcomes, including unsuccessful or unresolved records.

| File | Description |
| --- | --- |
| [`union_certification_short.csv`](data/union/union_certification/union_certification_short.csv) | Six weights $a_1,\ldots,a_6$ per row; **no header** |
| [`union_certification_short.pkl`](data/union/union_certification/union_certification_short.pkl) | Short records containing equation degree and six ambient weights |
| [`union_certification_medium.pkl`](data/union/union_certification/union_certification_medium.pkl) | Condensed singularity data for the certified terminal families |
| [`union_certification_long.pkl`](data/union/union_certification/union_certification_long.pkl) | More detailed singularity and certification records |
| [`union_certification_raw.pkl`](data/union/union_certification/union_certification_raw.pkl) | Raw certification records, including terminality-test outcomes |

The short CSV contains one row per weight vector, for example:

```csv
1,1,5,25,37,68
```

This represents the hypersurface $X_{136}\subset\mathbb{P}(1,1,5,25,37,68)$; the equation degree is recovered from $d=\sum_i a_i-1$. The `.pkl` files are Python pickle files for use with the scripts and notebooks in [`code/`](code/).

### Full classification: Zenodo

The consolidated classification is published as a separate Zenodo dataset [4]:

**[Sporadic List of Terminal Fano 4-Fold Hypersurfaces in Weighted Projective Space of Index 1](https://doi.org/10.5281/zenodo.23837634)**  
**DOI:** [`10.5281/zenodo.23837634`](https://doi.org/10.5281/zenodo.23837634)

The SQL archive, **`terminal_fano_4fold_index1_sporadic.sql`**, contains the table `terminal_fano_4fold_index1_sporadic`. It records the equation degree and individual weights, canonical class, point and curve singularity baskets (organised by type), their sizes, and smoothness, quasismoothness, terminality and canonicality indicators. It also incorporates quasismooth reference families. This is a **sporadic list**, not a claim of completeness beyond $d\leq200$.

For an index-one family, the anticanonical volume is

$$
(-K_X)^4=\frac{d}{a_1a_2a_3a_4a_5a_6}.
$$

In the SQL data, `Degree` represents the exact rational volume and `Degree_dec` its decimal approximation.

After downloading the SQL file, it can be imported into SQLite (with the `sqlite3` command-line tool installed):

```bash
sqlite3 terminal_fano_4fold_index1_sporadic.db ".read terminal_fano_4fold_index1_sporadic.sql"
```

For example, the following retrieves all recorded nonquasismooth families with equation degree greater than $200$:

```sql
SELECT *
FROM terminal_fano_4fold_index1_sporadic
WHERE Equation_degree > 200 AND IsQsmooth = 0;
```

### Quasismooth reference classification

[`data/quasismooth/quasismooth_terminal.csv`](data/quasismooth/quasismooth_terminal.csv) contains the reference classification of quasismooth terminal Fano fourfold hypersurfaces of index one, used to initialise the heuristic searches. Its sources are the [Graded Ring Database (GRDB)](https://www.grdb.co.uk/) [2] and the classification by Gavin Brown and Alexander M. Kasprzyk [1].

## Large searched-point logs

The complete searched-point logs are too large for the GitHub repository and are available through the [**searched-point GitHub release**](https://github.com/marctruter/fano_hypersurface_deep/releases/tag/searched_points):

- `fixed_searched_points.csv`
- `dynamic_searched_points_episode_1.csv` through `dynamic_searched_points_episode_5.csv`
- `ablation_searched_points_episode_1.csv` through `ablation_searched_points_episode_5.csv`

## Reproducing the computations

1. Clone the repository:

   ```bash
   git clone https://github.com/marctruter/fano_hypersurface_deep.git
   cd fano_hypersurface_deep
   ```

2. Set up a Python environment with the packages imported by the relevant scripts and notebooks (including NumPy, pandas, Matplotlib and PyTorch where required).
3. Download any large searched-point logs required by the analysis from the [GitHub release](https://github.com/marctruter/fano_hypersurface_deep/releases/tag/searched_points).
4. Run the relevant scripts or notebooks in [`code/`](code/), checking their expected working directory and relative data paths before execution.

## Companion repository

The companion repository, [*Terminal Fano 4-fold Hypersurfaces*](https://github.com/marctruter/fano_hypersurface_exhaustive), contains the exhaustive classification of terminal Fano fourfold hypersurfaces of index one for $d\leq200$, including **77,387** nonquasismooth families. Its classification data is available in the [Zenodo exhaustive classification dataset](https://doi.org/10.5281/zenodo.23836799) [3]. The associated paper, *Terminal Fano 4-fold Hypersurfaces* [5], is in preparation.

## Citation

If you use the heuristic-search code or experimental data, please cite the associated paper [6] and the Zenodo sporadic dataset [4]. The methods for certifying terminality are also developed in the author's doctoral thesis [7].

If you use the exhaustive classification through degree $200$, please also cite the associated paper [5] and Zenodo classification dataset [3]. If you use the reference quasismooth classification, please also cite Brown–Kasprzyk [1] and the GRDB [2].

## References

[1] Gavin Brown and Alexander M. Kasprzyk, *Four-dimensional projective orbifold hypersurfaces*, *Experimental Mathematics* **25** (2016), no. 2, 176–193. https://doi.org/10.1080/10586458.2015.1054054.

[2] Gavin Brown and Alexander Kasprzyk, [Graded Ring Database](https://www.grdb.co.uk/).

[3] Marc Truter, *Classification of Terminal Fano 4-Fold Hypersurfaces in Weighted Projective Space of Index 1 up to Degree 200*, version 1.0 [Data set], Zenodo (2026). https://doi.org/10.5281/zenodo.23836799.

[4] Marc Truter, *Sporadic List of Terminal Fano 4-Fold Hypersurfaces in Weighted Projective Space of Index 1*, version 1.0 [Data set], Zenodo (2026). https://doi.org/10.5281/zenodo.23837634.

[5] Marc Truter, *Terminal Fano 4-fold Hypersurfaces*, in preparation.

[6] Marc Truter, *Terminal Fano 4-fold Hypersurfaces via Deep Reinforcement Learning*, [arXiv:2603.15437](https://arxiv.org/abs/2603.15437) (2026).

[7] Marc Truter, *Terminal Hypersurfaces in Weighted Projective Spaces*, PhD thesis, University of Warwick.

## Acknowledgements

This work was supported by the UK Engineering and Physical Sciences Research Council (EPSRC) under grant number EP/W523793/1.

## License

The source code is released under the [MIT license](LICENSE).
