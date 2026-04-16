# Gauge-Invariant Representation Holonomy Code

Reference code repository for the paper:

**Gauge-invariant representation holonomy**  
Vasileios Sevetlidis and George Pavlidis  
Athena Research Center

Project page: <https://vasiseve.github.io/Gauge-Invariant-Representation-Holonomy/>  
Paper repository: <https://github.com/vasiseve/Gauge-Invariant-Representation-Holonomy>

## Scope

This repository is intended to host the reproducibility code for representation
holonomy experiments, including:

- holonomy estimator implementation,
- model training scripts,
- evaluation and robustness probes,
- experiment configuration files,
- plotting scripts for paper figures,
- and instructions for regenerating tables and figures.

The companion project-page repository contains the website and manuscript
assets. This repository should contain the executable research code.

## Method Summary

Representation holonomy measures path-dependent feature geometry in neural
networks. Given a small closed loop in input space, the method estimates local
rotation-only transports between neighboring feature geometries, composes them
around the loop, and measures the deviation of the resulting holonomy matrix
from identity.

The estimator uses:

- global feature whitening to fix a gauge,
- shared midpoint neighborhoods for edge-wise stability,
- shared low-rank subspaces for local transport,
- SO-only Procrustes alignment to avoid reflection artifacts,
- and loop composition to measure accumulated twist.

## Repository Layout

```text
.
├── configs/              # Experiment configuration files
├── data/                 # Dataset notes only; raw data is not committed
├── notebooks/            # Optional exploratory notebooks
├── outputs/              # Generated outputs, ignored by Git
├── scripts/              # CLI entrypoints for training/evaluation/plotting
│   └── run_holonomy_experiments.py
├── src/
│   └── holonomy/         # Python package for estimator and utilities
├── tests/                # Unit and smoke tests
├── CITATION.cff
├── LICENSE
├── README.md
└── requirements.txt
```

## Installation

Create a fresh Python environment, then install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Once package code is added, install the local package in editable mode:

```bash
pip install -e .
```

## Reproducibility Plan

The initial release includes the standalone experiment script:

```bash
python scripts/run_holonomy_experiments.py
```

The script is adapted from the paper experiment code and is designed to run in
Colab or a local Python environment. It trains the models, computes holonomy
curves and ablations, and writes results to `holonomy_results/` locally or to
Google Drive when running in Colab.

Over time, this script can be split into smaller package modules and command
line entrypoints.

The code release should document exact commands for:

1. Training MNIST and CIFAR models.
2. Extracting layer representations.
3. Computing holonomy over loop families.
4. Running estimator ablations.
5. Computing CKA and robustness comparisons.
6. Regenerating paper figures and tables.

Suggested command structure:

```bash
python scripts/train.py --config configs/mnist_mlp.yaml
python scripts/compute_holonomy.py --config configs/cifar10_resnet18_layer2.yaml
python scripts/plot_figures.py --input outputs/results --out outputs/figures
```

## Citation

```bibtex
@inproceedings{sevetlidis2025gauge,
  title     = {Gauge-invariant representation holonomy},
  author    = {Sevetlidis, Vasileios and Pavlidis, George},
  booktitle = {International Conference on Learning Representations},
  year      = {2025}
}
```
