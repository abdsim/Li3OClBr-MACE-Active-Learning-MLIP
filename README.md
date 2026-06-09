# Li<sub>3</sub>OClBr MACE MLIP: Active Learning and PCA Dataset

This repository accompanies work on training a **MACE machine-learning interatomic potential (MLIP)** for the Li<sub>3</sub>OClBr solid-electrolyte system using an **active-learning workflow**. It contains the MACE active-learning iterations, DFT-labelled structures used to improve the potential, and additional PCA-analysis datasets used to assess the diversity of grain-boundary, amorphous, and defect-containing configurations.

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
│
└── PCA_Analysis/
    ├── Amorphous_validation_dataset/
    └── Defects_validation_dataset/
```

---

## Overview

The goal of this repository is to document the development of a MACE MLIP for Li<sub>3</sub>OClBr. The workflow combines initial structure generation, MACE model training, MACE-driven molecular dynamics, exploration of new atomic environments, and DFT relabelling of selected structures. The dataset was improved iteratively so that the potential sampled increasingly diverse and physically relevant configurations of the Li<sub>3</sub>OClBr system.

The repository is divided into two main parts:

- **`MACE_Active_Learning/`** contains the active-learning iterations used to train and improve the MACE potential.
- **`PCA_Analysis/`** contains additional datasets used for PCA-based analysis of structural diversity and validation coverage.

---

## Active-learning workflow

The active-learning workflow follows the general loop after generating the initial dataset:

```text
Train MACE model → Run MACE-driven MD → Explore/select new structures → Label with DFT → Retrain MACE model
```

### `0_RAG_Structure_Generator/`
Located in `MACE_Active_Learning/1_iteration/`, this folder contains the workflow used to generate the initial dataset for the first MACE training iteration.

### `1_training/`
Contains the MACE training files for each iteration. These folders may include training configurations, input datasets, trained model files, logs, and model-error outputs.

### `2_md/`
Contains molecular dynamics simulations performed using the MACE potential from the corresponding iteration. These simulations were used to sample additional atomic environments beyond the current training set.

### `3_exploration/`
Contains structures selected from the MD/exploration stage. These configurations were used to identify new or underrepresented regions of configurational space for further evaluation.

### `4_dft/`
Contains DFT-labelled structures selected from the exploration stage. The resulting reference energies, forces, and/or stresses were added to the training data for the next active-learning iteration.

---

## PCA-analysis datasets

The `PCA_Analysis/` folder contains additional datasets used to compare the structural diversity of new configurations against the training data.

The PCA datasets include newly generated grain-boundary and defect configurations for Li<sub>3</sub>OCl, Li<sub>3</sub>OCl<sub>0.50</sub>Br<sub>0.50</sub>, and Li<sub>3</sub>OBr. The grain boundaries were constructed along 2-, 4-, and 6-fold rotation axes with coincident-site-lattice values up to Σ15, while the defect structures include vacancies, anion swaps, and disordered configurations.

### `Amorphous_validation_dataset/`

Contains amorphous validation structures used to test the MACE potential on disordered environments not limited to crystalline configurations.

### `Defects_validation_dataset/`

Contains defect-containing validation structures, including configurations with vacancies, anion swaps, and disorder.

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

The exact inputs, dataset paths, model settings, and output files depend on the specific active-learning iteration.

---

## Data description

Depending on the folder, the repository may contain:

- Initial structures generated for the first training dataset
- MACE training scripts and input/output files
- Trained MACE model files and training logs
- Selected exploratory structures
- DFT-labelled configurations
- PCA-analysis datasets for amorphous, grain-boundary, and defect-containing structures

---

## Citation

Please cite the following study or this repository if you make use of the files available in this repository:

Abdullah Bin Faheem and Haobo Li. "Machine-Learning-Potential-Driven Volcano Relationship in Grain Boundary Amorphicity and Ionic Transport of Antiperovskite Solid Electrolytes." Journal XXX (20XX): XX-XX.

Abdullah Bin Faheem and Haobo Li (2026). Li3OClBr-MACE-Active-Learning-MLIP (Version 1.0) [Data set]. GitHub. https://github.com/abdsim/Li3OClBr-MACE-Active-Learning-MLIP

## License

The data in this repository are licensed under the Creative Commons Attribution–NonCommercial 4.0 International License (CC BY-NC 4.0).

You may copy, redistribute, modify, and use the dataset, including for training machine-learning models, for noncommercial purposes.

When sharing the dataset or a modified version, you must give appropriate credit to the dataset creators.

When publishing research based on this dataset, please use the citation provided in the Citation section above.

This license applies only to the dataset and associated metadata. It does not apply to third-party software, third-party datasets, or other materials identified as having separate licensing terms.

Commercial use is not permitted under CC BY-NC 4.0. Requests for separate commercial permission should be submitted by opening an issue in this repository.
