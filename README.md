# radiomics-for-srs-external-validation-data-share
Open-source sample labels and positive label confidences data associated with the results presented in the manuscript "Dual-centre validation of using magnetic resonance imaging radiomics to predict stereotactic radiosurgery outcomes"


## Data Description

### Root Directory
**Ground Truth Labels.xlsx** - Provides a list of the patient and brain metastasis ID for each brain metastasis (sample) in the study for centres A and B. Samples are uniquely identified using the patient ID and metastasis ID pair. Samples with patient IDs > 10000 are from centre A. For each sample, the ground truth label is provided. If the value is "1", the sample is positive, meaning that the brain metastasis progressed post-SRS. Otherwise the sample is negative.

### A. Model external validation
Each file contains the positive label confidences from the machine learning model for each sample for all the experiments performed for "model external validation" (a model trained with one centre's data and tested with another centre's data).
The filename describes which centre's data (A or B) was used for training, and which was used for testing.
It also describes which features were used: "Clinical Features", "Radiomic Features", or "All Features" (clinical and radiomic features).
Lastly, the filename describes if the positive label confidences are from the training dataset's out-of-bag samples ("OOB Dataset Results") or the testing dataset's samples ("Testing Dataset Results").

### B. Methodology external validation
Each file contains the confidences for all the experiments performed for "methodology external validation" (a model trained and tested with one centre's data via bootstrapped resampling, but the methodology to train the model was developed at an independent centre).
The filename describes which centre the results are from, the features used, and whether the confidences are from the training out-of-bag samples or testing samples, as with "A. Model external validation".
As bootstrapped resampling was performed, each of the 250 iterations had their own results, which are stored in separate sheets within each file.
The training and testing on the entire dataset results needed to calculate the AUC_0.632+ correction are also included in a separate sheet.

### C. Pooled data validation
These files are very similarly laid-out to "B. Methodology external validation", except for "pooled data validation" (data from both centre's pooled and then used with bootstrapped resampling to train and test models), and so all filenames are marked with "Centres A & B".

### D. Feature harmonization and consolidation
These files are laid-out in a similar fashion to "A. Model external validation", but are from when ComBat harmonization or feature consolidation was performed, as indicated in each filename.
For the feature consolidation results, separate sheets provide the results for each experiment with the top n features included for n = 1 to 10.


## Data Usage

With the data shared within this repository, a user would be able to reproduce the full error metric analysis presented in the accompanying manuscript.
For each experiment, the positive label confidences and ground truths labels for the OOB datasets can be used to construct a receiver operating characteristic (ROC) curve based on the training dataset to choose an optimal operating point.
The positive label confidences and ground truths labels from the testing dataset can then be used to construct an ROC curve based on the testing dataset.
The area-under-the-ROC-curve (AUC) can be found directly from this ROC curve, and the misclassification rate, false negative rate, and false positive rate can be found using the optimal operating point found using the OOB dataset previously.
The positive label confidences and ground truths labels per iteration for bootstrapped resampled testing datasets can also be used to calculate the corrected AUC_0.632+ value.


## Contact Information
Author: David A. DeVries

Email: ddevrie8@uwo.ca

Organization: Western University/London Health Sciences Centre, London ON CA