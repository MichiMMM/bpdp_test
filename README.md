# Usage of this repository
This repository is supposed to help to reproduce the work proposed in the paper "Business Process Deviation Prediction: Predicting Non-Conforming Process Behavior"

The file "BPDP_Code.ipynb" contains all code used to implement and evaluate the proposed approach. The function "BPDP_classification_CIBE" executes the approach using the complex index-based encoding while the function "BPDP_classification_MPPN" uses the pre-trained feature vectors from MPPN. This folder contains all event logs, to-be models, and frozen alignments. Please load the respective data from the folder "Datasets" before. 

To train BPDP using the feature vectors created by MPPN:
- Train the MPPN using the code from https://github.com/joLahann/mppn
- Store the feature vectors per prefix in a pandas dataframe. Each row represents one prefix where "idx" is the unique id of the prefix and "FV" the learned feature vector of it

The folder "Evaluation" contains all evaluation results displayed in the paper. 

# Further Shapley value plots
The following graphs show Shapley value plots for all deviations of the BPIC 12A event log. 

## ('>>', 'A_APPROVED')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Model_A_APPROVED.png)

## ('A_APPROVED', '>>')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Log_A_APPROVED.png)

## ('>>', 'A_DECLINED')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Model_A_DECLINED.png)
