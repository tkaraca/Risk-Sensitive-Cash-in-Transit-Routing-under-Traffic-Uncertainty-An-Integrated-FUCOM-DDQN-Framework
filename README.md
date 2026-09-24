# REV16 Dynamic Cash-in-Transit Routing

This repository contains the minimal reproducible package for training and testing the REV16 dynamic cash-in-transit (CIT) vehicle-routing model.

The implementation uses a hierarchical, preference-conditioned Deep Q-Network for routing multiple CIT vehicles under time-window, capacity, travel-time, security-risk, and depot-return constraints.

## Required downloads

Download and extract both archives into the same directory:

1. `01_REV16_CODE.zip` — source code, dependencies, and documentation.
2. `02_REV16_DATA.zip` — the nine NumPy matrices required by the environment.

Both archives create and merge into the same `github_minimal_rev16` folder.

## Expected directory structure

```text
github_minimal_rev16/
|-- README.md
|-- requirements.txt
|-- vrp_cit_besiktas_HIERARCHICAL_CIT_REV16_QPRIMARY_EMERGENCY_FINETUNE.py
`-- cache_np/
    |-- distance.npy
    |-- risk.npy
    |-- velocity_std.npy
    |-- Saat8ort.npy
    |-- Saat10ort.npy
    |-- Saat12ort.npy
    |-- Saat14ort.npy
    |-- Saat16ort.npy
    `-- Saat18ort.npy
```

## Dataset

The `cache_np` directory contains the numerical matrices originally prepared from the Excel workbooks:

- network-distance matrix;
- edge-security-risk matrix;
- travel-speed standard-deviation matrix;
- time-dependent mean-speed matrices for 08:00, 10:00, 12:00, 14:00, 16:00, and 18:00.

The original Excel files are not required. The program checks `cache_np` first and directly loads these sanitized NumPy matrices.

## Requirements

- Python 3.10 or 3.11 is recommended.
- A TensorFlow-compatible CPU or GPU environment.
- Sufficient memory for the network matrices and replay buffer.

Create a virtual environment and install the dependencies:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

On Linux or macOS, activate the environment with:

```bash
source .venv/bin/activate
```

## Training and testing

Open a terminal inside the `github_minimal_rev16` directory and run:

```powershell
python vrp_cit_besiktas_HIERARCHICAL_CIT_REV16_QPRIMARY_EMERGENCY_FINETUNE.py
```

No pretrained `.h5` model is included. If no local checkpoint is present, the program starts training from scratch and then runs its configured testing workflow.

To view the available command-line arguments, run:

```powershell
python vrp_cit_besiktas_HIERARCHICAL_CIT_REV16_QPRIMARY_EMERGENCY_FINETUNE.py --help
```

## Generated files

Depending on the configuration, execution may create trained model weights, training and testing metrics, run logs, resumable checkpoints, and best-checkpoint directories. These generated artifacts are excluded by `.gitignore`.

## Reproducibility

Keep the data package unchanged and record the random seed and command-line arguments used for every experiment. Results may still vary across hardware and TensorFlow versions because some numerical operations can be nondeterministic.

## License

No explicit software license is included. Add an appropriate `LICENSE` file before permitting reuse or redistribution.
