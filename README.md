# Deep Reinforcement Learning for Fano Hypersurfaces
We design a deep reinforcement learning algorithm to explore a high-dimensional integer lattice with sparse rewards, training a feedforward neural network as a dynamic search heuristic to steer exploration toward reward dense regions. We apply this to the discovery of Fano 4-fold hypersurfaces with terminal singularities, objects of central importance in algebraic geometry. Fano varieties with terminal singularities are fundamental building blocks of algebraic varieties, and explicit examples serve as a vital testing ground for the development and generalisation of theory. Despite decades of effort, the combinatorial intractability of the underlying search space has left this classification severely incomplete. Our reinforcement learning approach yields thousands of previously unknown examples, hundreds of which we show are inaccessible to our search methods.

This is the repository for the source code and data associated to the paper: 

*Deep Reinforcement Learning for Fano Hypersurfaces*, [arXiv](https://arxiv.org/abs/2603.15437)

## Code

**Exhaustive Search** 
- `code/fano_exhaustive.py` search code
- `code/fano_exhaustive_analysis.ipynb` analysis code
  
**Fixed Heuristic Search**
- `code/fano_main.py` search and analysis code
  
**Dynamic Heuristic (Deep Reinforcement Learning) Search**
- `code/fano_main.py` search and analysis code

**Appendix**
- `code/fano_appendix_analysis.ipynb` analysis code

## Data

All data from the experiments is already in the repository in the `/data` folder, except for the two searched point dataset files due to their size. These are hosted on [GitHub Releases](https://github.com/marctruter/deep_fano_hypersurface/releases) and can be downloaded directly via:
- [fixed_searched_points.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/fixed_searched_points.csv)
- [dynamic_searched_points_episode_1.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/dynamic_searched_points_episode_1.csv)
- [dynamic_searched_points_episode_2.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/dynamic_searched_points_episode_2.csv)
- [dynamic_searched_points_episode_3.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/dynamic_searched_points_episode_3.csv)
- [dynamic_searched_points_episode_4.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/dynamic_searched_points_episode_4.csv)
- [dynamic_searched_points_episode_5.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/dynamic_searched_points_episode_5.csv)
- [ablation_searched_points_episode_1.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/ablation_searched_points_episode_1.csv)
- [ablation_searched_points_episode_2.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/ablation_searched_points_episode_2.csv)
- [ablation_searched_points_episode_3.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/ablation_searched_points_episode_3.csv)
- [ablation_searched_points_episode_4.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/ablation_searched_points_episode_4.csv)
- [ablation_searched_points_episode_5.csv](https://github.com/marctruter/deep_fano_hypersurface/releases/download/v1.0/ablation_searched_points_episode_5.csv)

Place both files in the `/data` folder.

**Quasismooth Classification**
- `/data/qs_terminal.csv` classification of quasismooth terminal Fano 4-fold hypersurfaces with Fano index 1

**Exhaustive Search**
- `/data/exhaustive_terminal_points.csv` terminal points found by the search
  
**Fixed Heuristic Search**
- `/data/fixed_settings.json` constants used
- `/data/fixed_terminal_points.csv` terminal points found by the search
- `/data/fixed_searched_points.csv` searched points
- `/data/fixed_reward_vs_steps.csv` number of terminal points found against step count
  
**Dynamic Heuristic (Deep Reinforcement Learning) Search**
- `/data/dynamic_settings.json` constants and hyperparameters used
- `/data/dynamic_terminal_points_episode_i.csv` terminal points found by the search
- `/data/dynamic_terminal_points_total.csv` terminal points over all episodes
- `/data/dynamic_searched_points_episode_i.csv` searched points
- `/data/dynamic_reward_vs_steps_episode_i.csv` number of terminal points found against step count
- `/data/dynamic_model.pth` neural network model at the final step of the search

**Analysis**
- `/data/fixed_differing_points.csv` terminal points found in the fixed but not dynamic search
- `/data/dynamic_differing_points_episode_i.csv` terminal points found in the dynamic but not fixed search
- `/data/fixed_differing_distances.csv` closest distances of terminal points found in the fixed but not dynamic search to their neighbours
- `/data/dynamic_differing_distances_episode_i.csv` closest distances of terminal points found in the dynamic but not fixed search to their neighbours

**Appendix**
- `/data/ablation_settings.json` constants and hyperparameters used
- `/data/ablation_terminal_points_episode_i.csv` terminal points found by the search
- `/data/ablation_searched_points_episode_i.csv` searched points
- `/data/ablation_reward_vs_steps_episode_i.csv` number of terminal points found against step count
- `/data/ablation_differing_points_episode_i.csv` terminal points found in the ablation but not fixed search
- `/data/ablation_differing_distances_episode_i.csv` closest distances of terminal points found in the ablation but not fixed search to their neighbours




