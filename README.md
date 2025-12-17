# Introduction-to-Deep-Learning Final Project
## Drug Response Prediction with Two-Tower Model
This project implements a deep learning solution to predict drug response (IC50 values) for various cancer cell lines. It utilizes a Two-Tower Neural Network architecture to learn latent representations of both cell lines and drugs, enabling the prediction of potential treatment efficacy
## Project Overview
The core objective of this project is to model the interaction between cancer cells and therapeutic compounds. By treating drug response prediction as a recommendation problem, the model uses:
  - **Cell Tower**: Encodes genomic and tissue-specific features of cell lines
  - **Drug Tower**: Encodes drug identifiers and target pathway information
  The model is trained to minimize the Mean Squared Error (MSE) between the predicted interaction score and the actual normalized IC50 value (transformed into a "Reward" metric)
## Dataset that we use
- **GDSC2-dataset.csv**: The primary dataset containing drug response data (IC50 values)
- **Cell_Lines_Details.xlsx**: Detailed metadata for cell lines, including tissue descriptors
- **Compounds-annotation.csv**: Annotation data for drugs, including target pathways
## Features that we select
- **COSMIC_ID**
- **GDSC Tissue descriptor 1**
- **DRUG_ID**
- **DRUG_NAME**
- **TARGET_PATHWAY**
- **LN_IC50**
## Model Architecture
1. Cell Branch:
  - Input: Cell Line ID, Tissue Descriptor
  - Layers: Embedding layers followed by a multi-layer perceptron (Dense -> ReLU -> Dense)  
2. Drug Branch:
  - Input: Drug ID, Target Pathway
  - Layers: Embedding layers followed by a multi-layer perceptron (Dense -> ReLU -> Dense)
    
The output vectors from both towers are combined using a dot product to generate a final scalar prediction (score). This score represents the predicted reward (efficacy).
## Workflow
1. **Data Loading**
   - Loads and merges the drug response data with cell and drug metadata
2. **Preprocessing**
   - Handled missing values
   - Label-Encoding features
   - IC50 values are normalized and inverted to create a Reward score (0 to 1), where higher values indicate better drug efficacy 
3. **Training**
   - Split the dataset into 80/20(train/test)
   - Using the Adam optimizer and MSE Loss
4. **Evaluation**
   - Evaluated using Root Mean Squared Error (RMSE)
5. **Visualization**
   - Training loss curves and reward distribution plots are generated to analyze convergence and prediction accuracy
## Baseline Comparison
- **Random Choice**: Simulates random guessing of rewards
- **Mean Choice**: Simulates always predicting the average reward of the dataset
## Frontend
- Using gradio to make the user interface to drug recommender
