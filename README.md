# Li<sub>3</sub>OCl<sub>1-x</sub>Br<sub>x</sub> MACE MLIP

This repository accompanies work on training a MACE machine learning interatomic potential (MLIP) for the Li<sub>3</sub>OCl<sub>1-x</sub>Br<sub>x</sub> solid-electrolyte system using an active-learning workflow. It contains the MACE active-learning iterations, DFT-labelled structures used to improve the potential, PCA datasets used to assess the diversity of the training data, evaluation datasets, python scripts, molecular dynamics inputs/outputs, and figure source data.

---

## File structure

```text
Li3OClBr-MACE-Active-Learning-MLIP/
├── README.md
├── MACE_Active_Learning/
│   ├── 1_iteration/
│   │   ├── 0_RAG_Structure_Generator/
│   │   ├── 1_training/
│   │   ├── 2_md/
│   │   ├── 3_exploration/
│   │   └── 4_dft/
│   ├── 2_iteration/
│   │   ├── 1_training/
│   │   ├── 2_md/
│   │   ├── 3_exploration/
│   │   └── 4_dft/
│   └── 3_iteration/
├── Evaluation_Datasets/
├── PCA_Analysis/
├── Codes/
├── Molecular_Dynamics/
│   ├── Bulk_Electrolyte/
│   ├── Grain_Boundary_Systems/
│   └── model.pt
└── Figure_Data/
```

---

## Overview

The repository is divided into several main parts:

- **`MACE_Active_Learning/`** contains the active-learning iterations used to train and improve the MACE potential.
- **`Evaluation_Datasets/`** contains the evaluation datasets for grain-boundary systems, bulk systems containing defects, and amorphous configurations.
- **`PCA_Analysis/`** contains additional datasets used for PCA-based analysis of structural diversity and validation coverage. The `Amorphous` and `Defective` datasets were compared with the training data.
- **`Codes/`** contains the python scripts utilized in our work.
- **`Molecular_Dynamics/`** contains molecular dynamics inputs and outputs for bulk systems and systems containing grain boundaries. It also includes the model used to run molecular dynamics simulations with LAMMPS.
- **`Figure_Data/`** contains Excel files with the figure source data for our work.

---

## Active-learning workflow

The active-learning workflow follows the general loop after generating the initial dataset:

```text
Train MACE model → Run MACE-driven MD → Explore/select new structures → Label with DFT → Retrain MACE model
```

### `0_RAG_Structure_Generator/`

Located in `MACE_Active_Learning/1_iteration/`, this folder contains the workflow used to generate the initial dataset for the first MACE training iteration.

### `1_training/`

Contains the MACE training files for each iteration. These folders may include datasets, training inputs/outputs from MACE, and trained model files.

### `2_md/`

Contains molecular dynamics simulations input/outputs performed using the MACE potential from the corresponding iteration. These simulations were used to sample additional atomic environments beyond the current training set.

### `3_exploration/`

Contains structures selected from the MD/exploration stage. These configurations were used to identify new or underrepresented regions of configurational space for further evaluation.

### `4_dft/`

Contains DFT-labelled structures selected from the exploration stage. The resulting reference energies and forces were added to the training data for the next active-learning iteration.

---

## Evaluation datasets

The **`Evaluation_Datasets/`** directory contains datasets used to evaluate the trained MACE potential across three classes of atomic configurations:

- Grain-boundary systems
- Bulk systems containing defects
- Amorphous configurations

---

## PCA analysis

The **`PCA_Analysis/`** directory contains two additional datasets, **Amorphous** and **Defective**, which were compared with the training data to assess structural diversity and validation coverage using PCA. The Amorphous dataset contains structures obtained from molecular dynamics simulations at 2000 K using the trained MACE MLIP without DFT labelling.

---

## Software and installation

This work used **MACE version `0.3.12`**.

For MACE installation instructions, see the official MACE documentation:

<https://mace-docs.readthedocs.io/>

---

## Running training jobs

Training was run from the corresponding training directory using the prepared `train.py` file with the command:

```bash
conda activate mace_cueq
python train.py > train.out
```

The exact inputs, datasets, model settings, and output files depend on the specific active-learning iteration.

---

## Citation

Please cite the following study or this repository if you make use of the files available in this repository:

Abdullah Bin Faheem and Haobo Li. "Machine-Learning-Potential-Driven Volcano Relationship in Grain Boundary Amorphicity and Ionic Transport of Antiperovskite Solid Electrolytes." Journal XXX (20XX): XX-XX.

Abdullah Bin Faheem and Haobo Li (2026). Li3OClBr-MACE-Active-Learning-MLIP (Version 1.0). GitHub. https://github.com/abdsim/Li3OClBr-MACE-Active-Learning-MLIP.

## License

The data in this repository are licensed under the Creative Commons Attribution–NonCommercial 4.0 International License (CC BY-NC 4.0).

You may copy, redistribute, modify, and use the files in this repository for non-commercial purposes.

When sharing the files or their modified versions, appropriate credit should be given.

When publishing using these files, please use the citation provided in the section above.

This license does not apply to third-party software, third-party datasets, or other items identified as having separate licensing terms.

Requests for separate commercial permission should be submitted by opening an issue in this repository.
