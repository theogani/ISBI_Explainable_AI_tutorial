# General Guidelines for Explainability Analysis with Nearest-Neighbor Contrastive Explainer

Welcome to the notebook for explainability analysis using the Nearest Neighbor Contrastive Explainer (NNCE). The task focuses on differentiating between clinically significant (csPCa) and insignificant prostate cancer (ciPCa). This guide will help you understand the clinical case, set up your environment, download and prepare the data, and reproduce the results documented in the notebook.

## Case overview

### Objective
Use explanability method to interpret and improve a model's predictions for classification of clinically insignificant and significant prostate cancer based on radiomics features.

### Data
The original dataset is from Prostate Imaging: Cancer AI challenge, specifically the Public Training and development dataset (PICAI). You can find more information [here](https://pi-cai.grand-challenge.org/)

_Dataset characteristics:_
- MRI modality: T2-weighted (T2W) and diffusion weighted (DWI) images (axial view)
- AI-based whole prostate gland segmentation files
- Clinical data including age, prostate volume, Prostate Specific Antigen (PSA), and PSA density.

### Methods
The data used for training consists of radiomics features extracted from the MRI images with the [PyRadiomics](https://github.com/AIM-Harvard/pyradiomics) library. The labels indicate whether the cancer is clinically significant (1) or insignificant (0).

#### Preprocessing and feature selection:
- **Harmonization**: `COMBAT` method was applied for feature harmonization, making the them vendor agnostic.
- **Outlier Removal**: `PCA`-based methods were employed for outlier removal.
- **Feature Selection**:
    - `T-test`: Features that are not statistically significant between the groups were removed using a t-test.
    - `Correlation Analysis`: Highly collinear features (correlation coefficient > 95%) were removed to avoid multicollinearity issues.
    - `Repeated Elastic Net Technique (RENT)`: RENT was used for feature selection to identify the most relevant features for classification.

#### Model training
A `Support Vector Machine` (SVM) with linear kernel (cost =4) was trained to classify the data. A training-testing data split was repeated 5 times, where one third of the data was used for testing and the rest for training.

__Performance metrics__


|            | Precision | Recall | F1-Score | Support |
|------------|-----------|--------|----------|---------|
| **0**      | 0.88      | 0.82   | 0.85     | 327     |
| **1**      | 0.62      | 0.73   | 0.67     | 134     |
|            |           |        |          |         |
| **Accuracy**       |           |        |    0.79  | 461     |
| **Macro Avg**      | 0.75      | 0.77   | 0.76     | 461     |
| **Weighted Avg**   | 0.81      | 0.79   | 0.80     | 461     |



__Confusion Matrix__
|              | Predicted 0 | Predicted 1 |
|--------------|--------------|-------------|
| **Actual 0** | 267          | 60          |
| **Actual 1** | 36           | 98          |





> You can found more information regarding this work [here]()

## Downloading Data and Code

__Repository__:
The code and data are available in the GitHub repository. Clone the repository to your local machine or directly download the files needed.

__Data__:
Download the radiomics data and pre-trained model files and upload them to your Google Colab environment. The necessary files are:
- `pc_model.joblib`
- `RENT_selected.txt`
- `isbi_data.csv`

Upload these files as a single folder (i.e. `case_one`) in the main folder of Google Drive
For the EDA part you also need to unzip first the `images.zip` file and include the folder `images` in the folder you will upload.

### Running the Notebook in Google Colab

Steps to Run:
1. Open the notebook
2. Run the required cells to mount GDrive and install the libraries
3. Load Data and Model
    - Load the radiomics data and the pre-trained SVM model.
    - The data is already normalized and clean.
4. Initialize and Train NNCE
5. Select a Sample:
    - Define a function to select a sample either randomly or by class label (clinically significant was selected as an example for the notebook).
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

