# Local-Minima-Preserving Polynomial Relaxation of Ising Problems

> **Accepted at the International Conference on Machine Learning (ICML) 2026**
> 
> **Authors:** Debraj Banerjee, Santanu Mahapatra, Kunal N. Chaudhury

Official code repository for the paper "Local-Minima-Preserving Polynomial Relaxation of Ising Problems" introducing MiP-CRIM.

## Overview
`MiP-CRIM` (Minima Preserving Continuous Relaxation of Ising Model) : Solver for Ising model optimization problems, including MAX-CUT, Number Partitioning Problem (NPP), Sherrington-Kirkpatrick (SK) models, and complete graphs.

## Files

- `ICML_paper.pdf` : arXiv version of the Paper
- `benchmark_SK.py` : benchmark runner and summary table output
- `demo_run.ipynb` : interactive Jupyter notebook demonstrating MiP-CRIM on SK, Complete Graph ($K_n$), G-set, and NPP models
- `quick_run.py` : straightforward quick run example for MiP-CRIM
- `iamp_sk_solver.py` : implementation of IAMP (Incremental Approximate Message Passing) solver for spin-glas model [1]
- `mip_crim.py` : MiP-CRIM implementation
- `environment.yml` : Conda environment
- `G10_graph.txt` : 800 nodes, 94.01\% sparse random graph with $\pm 1$ edge-weights from G-set dataset (https://web.stanford.edu/~yyye/yyye/Gset/)

1. **Install Conda**: Download [Miniconda](https://docs.conda.io/en/latest/miniconda.html) if needed.

2. **Create Environment**:

```bash
conda env create -f environment.yml
conda activate mip-crim
python quick_run.py
python benchmark_SK.py
```

## Fixed Parameters

The benchmark uses the following fine-tued hyperparameters, which are fixed throughout every test case so both methods are compared under a consistent setup.

- IAMP: `beta=6.0`, `delta=0.02`, `n_restarts=15`.
- MiP-CRIM: `T=10`, `K=200`, `alpha=0.000014996` ($\alpha$), `beta=0.001` ($\beta$), `lambda_=0.0707` ($\lambda$), `step=1.0` ($\tau$, ADAM learning rate), `beta1=0.09` ($\beta_1$, 1st moment for ADAM), `beta2=0.999` ($\beta_2$, 2nd moment for ADAM), `eps=1e-8`, `sigma_noise=1e-3`.

- The elements $J_{ij}$ in the SK model are rounded to 5th decimal places so that $lsb = 10^{-5}$ and we get thebound $\gamma_0 = 10^{-5}$, satisfying the admissibility condition: $3\beta\lambda^2 < \alpha < \beta\lambda^2 + \gamma_0$ for the MiP-CRIM parameters.

## Notes

The benchmark uses both type of SK models:

- **Gaussian Orthogonal Ensemble (GOE)** [[1]](#references): $J \in \mathbb{R}^{n\times n}$ where $J_{ij} = J_{ji} \sim \mathcal{N}[0, 1/n]$ for $i\neq j$ and $J_{ii} \sim \mathcal{N}[0, 2/n]$.
- **Standard**: $J_{ij} \sim \mathcal{N}[0, 1]$ with $J_{ij} = J_{ji}$ and zero diagonal.

## Citation

If you find this code useful in your research, please consider citing our paper:
```bibtex
@inproceedings{banerjee2026local,
  title={Local-Minima-Preserving Polynomial Relaxation of Ising Problems},
  author={Banerjee, Debraj and Mahapatra, Santanu and Chaudhury, Kunal N.},
  booktitle={International Conference on Machine Learning (ICML)},
  year={2026}
}
```

## References

[1] "Optimization of the Sherrington-Kirkpatrick Hamiltonian." *arXiv:1812.10897v2*.
