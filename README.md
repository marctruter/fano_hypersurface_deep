# Terminal Fano 4-fold Hypersurfaces via Deep Reinforcement Learning

**Source code and data for [*Deep Reinforcement Learning for Fano Hypersurfaces*](https://arxiv.org/abs/2603.15437).**

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

The paper describes the search algorithms, terminality certification, distance analysis and ablation experiments.

## Repository structure

```text
code/                                  Search and analysis scripts/notebooks

data/
  quasismooth/
    quasismooth_terminal.csv            Reference quasismooth classification
  fixed/                                Fixed-search results and certification data
  dynamic/                              Dynamic-search results and certification data
  ablation/                             Ablation-search results
  union/
    union_certification/
      union_certification_short.csv     Unique weight vectors (no header)
      union_certification_short.pkl     Degree and weight records
      union_certification_medium.pkl    Condensed singularity records
      union_certification_long.pkl      Detailed certification records
      union_certification_raw.pkl       Raw records and certification outcomes

figures/                                Figures generated for the paper
LICENSE                                 MIT licence
README.md
```

The tree highlights the principal directories and consolidated certification files; it is not a complete listing of experimental outputs.

## Classification and certification data

### Combined heuristic-search datasets

The files in [`data/union/union_certification/`](data/union/union_certification/) combine the fixed search and all five dynamic runs. Processed datasets contain distinct certified terminal families, identified by their weight vectors. The raw dataset retains certification outcomes, including unsuccessful or unresolved records.

| File | Description |
| --- | --- |
| `union_certification_short.csv` | Six weights $a_1,\ldots,a_6$ per row; **no header** |
| `union_certification_short.pkl` | Short records containing equation degree and weights |
| `union_certification_medium.pkl` | Condensed singularity data for the certified families |
| `union_certification_long.pkl` | More detailed certification data |
| `union_certification_raw.pkl` | Original records, including terminality-test outcomes |

The short CSV has one row per weight vector, for example:

```csv
1,1,5,25,37,68
```

This represents $X_{136}\subset\mathbb{P}(1,1,5,25,37,68)$; the equation degree is recovered from $d=\sum_i a_i-1$. The `.pkl` files are Python pickle files intended for analysis with the accompanying code.

### Full classification: Zenodo

The consolidated classification **`terminal_fano_fourfolds_index1_sporadic.sql`** is distributed through **Zenodo**, rather than included in this GitHub repository.

**Zenodo record / DOI:** *Link to be added after publication.*

The SQL archive records equation degrees, individual weights, canonical classes, exact and decimal anticanonical volumes, point and curve singularity baskets, and smoothness, quasismoothness, terminality and canonicality indicators. Its classification also includes quasismooth reference entries where applicable.

For an index-one family, the anticanonical volume is

$$
(-K_X)^4=\frac{d}{a_1a_2a_3a_4a_5a_6}.
$$

In the SQL data, `Degree` stores this number as an exact rational string, and `Degree_dec` stores its decimal approximation. The singularity baskets are separated by type and by point or curve.

### Quasismooth reference classification

[`data/quasismooth/quasismooth_terminal.csv`](data/quasismooth/quasismooth_terminal.csv) contains the reference classification of quasismooth terminal Fano fourfold hypersurfaces of index one, used to initialise the heuristic searches. This reference data comes from the [Graded Ring Database (GRDB)](https://www.grdb.co.uk/forms/fano4ci1) and the classification by Gavin Brown and Alexander M. Kasprzyk in [*Four-dimensional projective orbifold hypersurfaces*](https://doi.org/10.1080/10586458.2015.1054054), *Experimental Mathematics* **25** (2016), no. 2, 176–193. Please cite these original sources when using the quasismooth dataset.

## Large searched-point logs

The complete searched-point logs are too large for the GitHub repository and are available through the [**searched-point GitHub release**](https://github.com/marctruter/fano_hypersurface_deep/releases/tag/searched_points):

- `fixed_searched_points.csv`
- `dynamic_searched_points_episode_1.csv` through `dynamic_searched_points_episode_5.csv`
- `ablation_searched_points_episode_1.csv` through `ablation_searched_points_episode_5.csv`

Download the logs needed for the relevant analysis and place them at the locations expected by the corresponding scripts or notebooks. They are not needed simply to inspect the consolidated classification data.

## Reproducing the analysis

1. Clone the repository:

   ```bash
   git clone https://github.com/marctruter/fano_hypersurface_deep.git
   cd fano_hypersurface_deep
   ```

2. Set up a Python environment with the packages imported by the relevant scripts and notebooks (including NumPy, pandas, Matplotlib and PyTorch where required).
3. Download any large searched-point logs required by the analysis from the GitHub release.
4. Run the relevant scripts or notebooks in `code/`, checking their relative input and output paths before execution.

The consolidated CSV and pickle datasets allow inspection of the search discoveries without rerunning the searches. The Zenodo SQL archive provides the full tabulated geometric data.

## Citation

If you use the code or data, please cite the associated paper:

**Marc Truter**, [*Deep Reinforcement Learning for Fano Hypersurfaces*](https://arxiv.org/abs/2603.15437), arXiv:2603.15437 (2026).

For the complete classification dataset, please also cite its Zenodo DOI once available. When using the quasismooth reference data, credit the [GRDB](https://www.grdb.co.uk/forms/fano4ci1) and [Brown–Kasprzyk (2016)](https://doi.org/10.1080/10586458.2015.1054054).

## Licence

The source code is released under the [MIT licence](LICENSE).
