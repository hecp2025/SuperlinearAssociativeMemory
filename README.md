# SuperlinearAssociativeMemory

Codebase for hardware-adaptive learning in memristor-based associative memory with a multilayer structure.

This repository accompanies the paper:

**A Hardware-Adaptive Learning Algorithm for Superlinear-Capacity Associative Memory on Memristor Crossbars**

---

## What’s inside

- **Hardware-adaptive (device-aware) training** for associative memory under device non-idealities  
  - `stuck`: stuck-at-fault ratio (or related fault rate)
- **Multilayer Hopfield-style associative memory** experiments (e.g., MNIST patterns)
- Utilities and a memristor simulation module

> Main entry script: `multilayer.py`

---

## Repository structure

Typical layout:

- `multilayer.py` — main script for training / evaluation (CLI)
- `HopfiledNetwork.py` — Hopfield(-style) network implementation
- `utils.py` — helper functions
- `memristor_simulation/` — memristor/device modeling utilities

---

## System requirements

### Operating systems
- Linux / Windows / macOS (recommended: Linux for best reproducibility)

### Software dependencies
- Python >= 3.9
- Key Python packages are listed in `requirements.txt` (see below)

### Tested on
- Please fill in with your actual environment once confirmed, e.g.:
  - Ubuntu 22.04, Python 3.10, torch 2.x, torchvision 0.x

### Non-standard hardware
- No non-standard hardware is required.
- (Optional) A CUDA-capable GPU can speed up experiments but is not required.

---

## Installation

```bash
git clone https://github.com/hecp2025/MultilayerAssociateMemory.git
cd MultilayerAssociateMemory

python -m venv .venv
# Windows:
#   .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```
Typical install time (normal desktop): ~5–20 minutes (mostly depends on network speed and installing PyTorch).

Demo: run on the provided setting (MNIST)
## Train
```bash
python multilayer.py \
  --dimension 64 \
  --interval 1 \
  --train-eval 'train' \
  --variation '0.0' \
  --stuck '0.0' \
  --corruption 0.05 \
  --seed 1 \
  --dataset 'mnist' \
  --binary True \
  --max-pattern 64 \
  --min-pattern 1
```
## Evaluate
```bash
python multilayer.py \
  --dimension 64 \
  --interval 1 \
  --train-eval 'eval' \
  --variation '0.0' \
  --stuck '0.0' \
  --corruption 0.05 \
  --seed 1 \
  --dataset 'mnist' \
  --binary True \
  --max-pattern 64 \
  --min-pattern 1
```

## Expected output

The script prints progress and evaluation metrics to the console (e.g., recall accuracy / capacity-related metrics).

If the code saves figures/results, specify the output path here (e.g., ./results/).

Expected runtime (normal desktop)

(Fill in after one run) e.g., max-pattern=64 typically completes in ~1–5 minutes on GPU.

## Key CLI arguments (summary)

--dimension: input dimension (MNIST flattened is 784)

--train-eval: 'train' or 'eval'

--dataset: dataset name (e.g., 'mnist')

--binary: whether to binarize patterns

--corruption: input corruption ratio / noise level for recall tests

--variation: device variation strength (0.0 = ideal)

--stuck: stuck-at-fault ratio / level (0.0 = no faults)

--max-pattern, --min-pattern: pattern count sweep range

--seed: random seed for reproducibility

--interval: logging / evaluation interval (implementation-defined)

## How to run on your own data

Prepare your dataset in the format expected by the code.

Add a new dataset option (or replace the MNIST loader) in the dataset-loading part of multilayer.py.

Run with --dataset <your_dataset_name> and adjust --dimension, --binary, and other flags accordingly.

## Citation

If you use this code in academic work, please cite the associated paper:

```bibtex
@article{multilayer_associate_memory,
  title   = {A Hardware-Adaptive Learning Algorithm for Superlinear-Capacity Associative Memory on Memristor Crossbars},
  author  = {Authors},
  journal = {To appear},
  year    = {2025},
}
