# Single-Cell RNA-Seq Analysis Project: Peripheral Blood Mononuclear Cells (PBMCs)

## Project Overview

This repository documents an introductory single-cell RNA sequencing (scRNA-seq) data analysis pipeline for Peripheral Blood Mononuclear Cells (PBMCs). The project aims to demonstrate fundamental steps in scRNA-seq analysis using Python and the `scanpy` library.

## Dataset

The analysis is performed on a publicly available dataset:

- Title: "5k Peripheral Blood Mononuclear Cells (PBMCs) from a Healthy Donor (v3 chemistry)"
- URL: https://www.10xgenomics.com/datasets/5-k-peripheral-blood-mononuclear-cells-pbm-cs-from-a-healthy-donor-v-3-chemistry-3-1-standard-3-0-2

## Software and Dependencies

This project is developed using Python and relies heavily on the `scanpy` library for single-cell data analysis. The environment is managed using `Conda`.

Key libraries include:

- `scanpy`
- `numpy`
- `pandas`
- `matplotlib`
- `leidenalg`
- `python-igraph`
- `scikit-learn` (dependency for some scanpy functions)

To set up the environment, use the provided `environment.yml` file:

```bash
conda env create -f environment.yml
conda activate scrnaseq_env
```

## Analysis Steps

The `01_initial_data_exploration.ipynb` Jupyter notebook covers the following core scRNA-seq analysis steps:

1.  **Data Loading and Initial Quality Control (QC):**
    - Loading raw count data.
    - Filtering out low-quality cells (based on mitochondrial content, total counts, and detected genes).
    - Filtering out unexpressed genes.
2.  **Normalization and Log-Transformation:**
    - Normalizing gene expression counts to account for sequencing depth differences.
    - Log-transforming the normalised data.
3.  **Feature Selection:**
    - Identifying and selecting highly variable genes (HVGs) for downstream analysis.
4.  **Data Scaling:**
    - Scaling gene expression values to ensure genes contribute equally to distance calculations.
5.  **Dimensionality Reduction:**
    - **Principal Component Analysis (PCA):** Linear reduction to identify major sources of variation. [Number of PCs chosen: **15**]
    - **UMAP (Uniform Manifold Approximation and Projection):** Non-linear reduction for 2D visualization of cell similarity.
6.  **Clustering:**
    - **Leiden Algorithm:** Graph-based clustering to group cells into distinct populations based on their similarity. [Resolution used: **0.5**]. [Number of clusters identified: **13**]
7.  **Cell Type Annotation:**
    - Identification of cluster-specific marker genes using differential gene expression analysis.
    - Manual assignment of biological cell type labels to each cluster based on canonical markers.

## Key Findings (Summary)

- Initial quality control effectively removed low-quality cells.
- Dimensionality reduction revealed distinct cell populations in the UMAP embedding.
- Leiden clustering identified **13** distinct cell clusters.
- Manual annotation, based on canonical marker genes, assigned preliminary identities to these clusters, including major immune cell types such as **CD4+ T cells, CD8+ T cells, B cells, Monocytes, NK cells, NKT cells, Memory B cells, Monocyte-derived DC / Macrophages, and Platelets**.
- Initial observations suggest good separation of clusters, including minor subpopulations, with Cluster 12 identified as potentially representing platelets or noise.

## How to Run This Project

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/adabyt/scrnaseq_analysis_project.git
    cd scrnaseq_analysis_project
    ```
2.  **Set up the Conda environment:**
    ```bash
    conda env create -f environment.yml
    conda activate scrnaseq_env
    ```
3.  **Download the dataset:**
    Download the `filtered_feature_bc_matrix.h5` file from the 10x Genomics website (link provided in the Dataset section above) and place it into a `data/` subdirectory within the project root (i.e., `scrnaseq_analysis_project/data/`).
4.  **Open and run the Jupyter Notebook:**
    ```bash
    jupyter lab
    ```
    Then, open `01_initial_data_exploration.ipynb` and run all cells sequentially.

## Future Work / Next Steps

As this project is for learning purposes, future explorations could include:

- Saving the final annotated `AnnData` object for quicker loading in future sessions.
- Performing more in-depth differential gene expression analysis between specific clusters.
- Investigating cell-cell communication using ligand-receptor analysis.
- Exploring potential cell differentiation trajectories (e.g., for the monocyte-derived populations).
- Integrating additional datasets or samples (e.g., from different conditions or donors).
- Comparing different clustering resolutions and their biological implications.
