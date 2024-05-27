General Guidelines for Reproducing Explainability Analysis with Nearest Neighbor Contrastive Explainer

Welcome to the notebook for explainability analysis using the Nearest Neighbor Contrastive Explainer (NNCE). The task focuses on differentiating between clinically significant and insignificant prostate cancer. This guide will help you understand the clinical case, set up your environment, download and prepare the data, and reproduce the results documented in the notebook.

1. Clinical Case Overview

Objective:
To differentiate between clinically significant and insignificant prostate cancer using radiomics data and interpret the model's predictions using explainability techniques.

Dataset:
The dataset consists of radiomics features extracted from prostate cancer patients. The labels indicate whether the cancer is clinically significant (1) or insignificant (0).

Model:
We use a pre-trained Support Vector Machine (SVM) model to classify the data. The model predicts whether a given set of radiomics features corresponds to clinically significant or insignificant prostate cancer.

2. Downloading Data and Code

Repository:
The code and data are available in the GitHub repository. Clone the repository to your local machine or directly download the files needed.

Data:
Download the radiomics data and pre-trained model files and upload them to your Google Colab environment. The necessary files are:
- pc_model.joblib
- RENT_selected.txt
- isbi_data.csv

- You should upload these files as a single directory in the main folder of Google Drive
- For the EDA part you need first to unzip the "images.zip" file

4. Running the Notebook in Google Colab

Steps to Run:
1. Open the notebook
2. Run the required cells to mount GDrive and install the libraries
3. Load Data and Model
    - Load the radiomics data and the pre-trained SVM model.
    - The data is already normalized and clean.
4. Initialize and Train NNCE
5. Select a Sample:
    - Define a function to select a sample either randomly or by class label (clinically significant or insignificant).
    - Perform explainability analysis on the selected sample.

6. Explainability Analysis:
    - Compute nearest clinically insignificant and significant contrastive instances.
    - Visualize the differences (delta) between the selected sample and its contrastive instances.
    - Perform additional analyses like global feature importance, explaining misclassifications, feature sensitivity analysis, and visualizing high-dimensional embeddings.

5. Understanding the Outputs

Explainability Analysis Outputs:
- Nearest Neighbors: Identification of nearest clinically insignificant and significant instances.
- Delta Visualization: Heatmaps showing the differences in features between the selected sample and its nearest neighbors.

- Global Feature Importance: Analysis of the most influential features across multiple samples.
- Misclassification Analysis: Understanding why certain instances were misclassified.
- Feature Sensitivity: Assessing how changes in specific features affect model predictions.
- Embedding Visualization: Using dimensionality reduction techniques to visualize the embedding space learned by NNCE.
