# Companion Notebook — Dual-Network PINN for Mass–Spring–Damper Optimal Control

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20404730.svg)](https://doi.org/10.5281/zenodo.20404730)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Tahimi/PINN-MSD-Optimal-Control/blob/main/PINN_MSD_Optimal_Control.ipynb)

Reproducible companion code for the paper:

> **Dual-Network PINNs for Optimal Control: A Reproducible Benchmark on the Mass–Spring–Damper System**
> Abdeladhim Tahimi, 2026.

## What this repository contains

This repository archives the complete computational pipeline used to produce every numerical result, table, and figure of the paper. The pipeline is implemented as a single Jupyter notebook designed for Google Colab.

- `PINN_MSD_Optimal_Control.ipynb` — the companion notebook.
- `README.md` — this file.
- `LICENSE` — MIT license terms.
- `CITATION.cff` — machine-readable citation metadata for GitHub's "Cite this repository" button.
- `requirements.txt` — Python package dependencies (with versions).

## Scope of the benchmark

The notebook implements three independent solution methods for the same constrained optimal control problem on a linear mass–spring–damper system:

1. **Pontryagin's Minimum Principle (PMP)** via single shooting — used as the gold reference solution.
2. **Direct transcription via trapezoidal collocation** solved as an NLP with SLSQP — used as an independent second classical reference.
3. **Dual-network Physics-Informed Neural Network (PINN)** with hard boundary-condition enforcement on the state via a composite ansatz, and an unconstrained control network.

All three methods are evaluated on a common dense reference grid; the PINN is validated against the two classical references via pointwise $L^2$ and $L^\infty$ errors and a comparison of the achieved cost.

## How to run

The notebook is designed to run on **Google Colab** without local setup.

### Option 1 — One-click on Colab

Click the "Open in Colab" badge at the top of this README. The notebook will open in Colab and you can run all cells in order.

### Option 2 — Local Jupyter

```bash
git clone https://github.com/Tahimi/PINN-MSD-Optimal-Control.git
cd PINN-MSD-Optimal-Control
pip install -r requirements.txt
jupyter notebook PINN_MSD_Optimal_Control.ipynb
```

If running locally, edit cell 2 to skip the Google Drive mount and point `PROJECT_ROOT` at a local folder of your choice.

## Reproducibility

A single global random seed (`SEED = 42`) is set for `numpy`, `torch` (CPU + CUDA), and Python's `random` module. All training results are bit-reproducible given the same seed and PyTorch version.

## Output files

After running the notebook, the following files are written into `<PROJECT_ROOT>/`:

```
results/
    trajectories.csv      # all three methods + pairwise errors, dense grid (501 pts)
    loss_history.csv      # PINN loss components vs iteration
figures/
    fig_state_x.pdf, .png         # displacement trajectory
    fig_state_v.pdf, .png         # velocity trajectory
    fig_control_u.pdf, .png       # optimal control
    fig_error_x.pdf, .png         # log-scale pointwise error in displacement
    fig_error_u.pdf, .png         # log-scale pointwise error in control
    fig_loss_history.pdf, .png    # training loss history
```

Each figure cell in the notebook is **self-contained**: it reads `trajectories.csv` (or `loss_history.csv`) from disk and rebuilds the plot from scratch. You can re-generate any single figure without re-executing the training pipeline.

## Citation

If you use this code or the accompanying paper, please cite both:

```bibtex
@article{tahimi2026pinnmsd,
  author  = {Tahimi, Abdeladhim},
  title   = {Dual-Network {PINNs} for Optimal Control: A Reproducible Benchmark on the Mass--Spring--Damper System},
  journal = {(in preparation)},
  year    = {2026},
}

@software{tahimi2026notebook,
  author    = {Tahimi, Abdeladhim},
  title     = {Companion Notebook for ``Dual-Network PINNs for Optimal Control: A Reproducible Benchmark on the Mass--Spring--Damper System''},
  year      = {2026},
  publisher = {Zenodo},
  version   = {v1.0.0},
  doi       = {10.5281/zenodo.20404730},
  url       = {https://doi.org/10.5281/zenodo.20404730}
}
```

## License

The code in this repository is released under the **MIT License**. See [LICENSE](LICENSE) for the full text. You are free to use, modify, and redistribute the code, including for commercial purposes, provided the copyright notice and license terms are preserved.

## Acknowledgments

During the development of this work, the author used AI-based language models (Claude, Anthropic, 2024–2026) as assistive tools for writing, code development, and computational verification. All conceptual and scientific decisions originated with the author, and all results were independently verified.

## Contact

Abdeladhim Tahimi — [GitHub profile](https://github.com/Tahimi)

For questions about the paper or the code, please open an issue on this repository.
