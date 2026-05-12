# A Lightweight Content-Based Phishing Detection Approach Using Cross-Model Knowledge Distillation
This repository contains documentation for the dataset, code, and methodology used in the manuscript titled: A Lightweight Content-Based Phishing Detection Approach Using Cross-Model Knowledge Distillation
# Abstract
Website phishing attacks present a complex security challenge, as the difficulty lies in distinguishing legitimate websites from phishing ones.
Despite the efforts of researchers to prevent phishing website attacks, current approaches still suffer from several major shortcomings, including:

- High computational cost.
- Lack of specialized web content analysis.
- Language-dependent detection limits generalizability.
- Features requiring third-party intervention.
- Limited analysis of the obfuscated JavaScript features.

To address these limitations, we propose the following contributions:

1- We provide a realistic dataset containing 32 content-based features, including indicators of JavaScript obfuscation extracted through static parsing of publicly available phishing and legitimate websites. The features are independent of language and third-party services.

2- We introduce a knowledge distillation-based approach for web content-based phishing detection by transferring expertise from a high-performing XGBoost teacher model to a lightweight MLP student model, an approach that has received limited attention in previous studies.

The proposed model achieves an average accuracy of **97.46%** on the test set across five runs, with an average computation time of **2.8516×10⁻⁶ seconds** per website and a model size of **0.17 MB**, demonstrating high performance with low computational cost.

### Steps to Reproduce the Results:
For reproducibility, all code files and the final processed dataset are provided as supplementary materials with the PeerJ Computer Science journal submission. 

**To quickly reproduce the reported results,** download the final dataset (*Final_dataset_32content_based_features.csv*) and run the model training notebook as follows:

1- Ensure the required environment is set up as described in the Requirements section (using the local machine and installing model training requirements).

2- Run the *Model_Training_Code_.ipynb*

This will directly reproduce the training and evaluation results using the processed dataset.

# Methodology

### Data Collection & Data Pre-processing: 
The dataset used in this study was collected from multiple sources. Legitimate URL data was obtained from publicly available datasets (e.g., Kaggle and Mendeley Data, while phishing URLs were collected using the PhishTank API. The API provides JSON reports of URLs, including both verified and unverified entries. Only URLs confirmed as live and verified phishing were retained. For phishing samples, web content was extracted using an API key in batches. Similarly, legitimate samples were also processed in batches. This approach was adopted to manage computational resources efficiently and to avoid interruptions or failures due to large volumes of requests. 

The collected data was then aggregated into a unified dataset. After feature extraction, the dataset contained:

- Legitimate dataset: 30,560 URLs
- Phishing dataset: 30,368 URLs

Data pre-processing steps (such as duplicate removal and handling missing values) and feature engineering, specifically feature selection, were applied. As a result, **a final dataset of 23,105 samples with 32 static content-based features was used for training and evaluation**. The labels are defined as: *Legitimate website = 0, Phishing website = 1*

### Feature Extraction:
Feature extraction was performed to convert raw web content into structured representations suitable for machine learning. An initial total of 41 static content-based features were extracted from each website, capturing structural and content-related characteristics used for phishing detection. The extracted features include information derived from Hypertext Markup Language (HTML) structure, embedded JavaScript, and external JavaScript files.

### Model Training: 
Model training was conducted using the processed dataset after feature extraction and pre-processing. Three models were developed and evaluated: a baseline Multilayer Perceptron (MLP), XGBoost, and a knowledge distillation approach (teacher-student learning), which applies the knowledge distillation from the XGBoost teacher to the MLP student to leverage the strong predictive capabilities of the XGBoost algorithm to enhance the performance of the MLP deep learning model while maintaining its lightweight nature for efficient web content analysis at a low computational cost. The models were trained on the selected feature set, and their performance was evaluated using standard classification metrics (Accuracy, Recall, Precision, F1-score, and Time).

# Requirements
### Hardware Dependencies:
The experiments were conducted using both a virtual machine and a local environment. Feature extraction was performed in a VirtualBox virtual machine while data pre-processing and model training were carried out on a local machine, equipped with an Intel Core i7-8565U processor (up to 1.99 GHz) and 16 GB of RAM, running Windows 11. All developments were carried out using Jupyter Notebook. 

### Software Dependencies:
- VirtualBox virtual machine: Python 3.11.5
- Local machine: Python 3.10.9

The main libraries used include:

Feature Extraction:
-	pandas (2.1.1)
-	Beautifulsoup4 (bs4 4.12.4)
-	urllib3 (1.26.20)
-	requests (2.31.0)
-	The lxml parser was used instead of the default html.parser for improved parsing performance.

Model Training: 
- pandas (2.1.1)
- numpy (1.26.4)
- TensorFlow (2.18.0)
- The baseline MLP and teacher-student models were implemented using TensorFlow/Keras, while XGBoost was implemented using the scikit-learn framework.

# Code Information  
Each file serves a specific purpose in the phishing website detection pipeline:

- *Data_Collection_Static_Content_Based_Features_Code_.ipynb*, this file contains the implementation of 41 initial static content-based features for phishing detection. It also includes the list of the 32 selected features, which were determined in a separate feature selection step and used for model training.
- *To_Extract_Static_Content_Based_Features_Code_.ipynb*, extracts features from phishing and legitimate URLs, including basic pre-processing and dataset preparation applied to the legitimate dataset, and produces structured labeled datasets.
- *Data_Preprocessing_Code_.ipynb*, performs pre-processing on the final phishing and legitimate dataset prepared in the previous step. This stage focuses on preparing the dataset for learning, including merging phishing and legitimate samples, shuffling, removing duplicates and missing values, correlation analysis, and feature selection.
- *Model_Training_Code_.ipynb*, the processed dataset is used to train and evaluate three models: a baseline MLP model, an XGBoost model, and a knowledge distillation approach combining both.
- *Final_dataset_32content_based_features.csv*, the final processed dataset used for training, evaluation, and reporting of results.

# Usage Instructions For Full Pipeline (Optional):

### Full Pipeline (Optional):
This section describes the full pipeline can be executed to regenerate the dataset from scratch, starting from data collection and feature extraction through to model training and evaluation, by following these steps:

1- **Feature Definition:** Run *Data_Collection_Static_Content_Based_Features_Code_.ipynb* to define and generate the initial 41 static content-based features.

2- **Feature Extraction and Dataset Preparation:** Run *To_Extract_Static_Content_Based_Features_Code_.ipynb* to extract features from phishing and legitimate URLs and generate structured labeled datasets.

3- **Data Pre-processing:** Run *Data_Preprocessing_Code_.ipynb* to perform final pre-processing, including handling missing values, duplicate removal, correlation analysis, and feature selection. 

4- **Model Training and Evaluation:** Run *Model_Training_Code_.ipynb*, which trains and evaluates the three models (MLP, XGBoost, and knowledge distillation approach). 

**Note:**
The selection of the 32 most important features is implemented within the training pipeline. Users may switch between using the full 41 features or the selected 32 features by commenting out the corresponding section in the code. 

**Additionally Note:**
The PhishTank API used for phishing data collection requires user registration on the PhishTank platform and API key access. Additionally, the full data collection and feature extraction pipeline is provided for completeness; however, its execution is optional and not required to reproduce the reported results, as the final processed dataset is included.


# **Acknowledgment**
Part of this work is based on an open-source implementation developed by *Biagio Montaruli et al. (2023)*, available at: extract_features_html.py, https://github.com/advmlphish/raze_to_the_ground_aisec23/blob/main/src/extract_features_html.py 

# Citations
The dataset used in this study:

1- Anil Singh. (2024). 45+ M Domains with size & Language - Common Crawl [Dataset]. Kaggle. https://doi.org/10.34740/KAGGLE/DSV/9615721

2- Ariyadasa, Subhash; Fernando, Shantha; Fernando, Subha (2021), “Phishing Websites Dataset”, Mendeley Data, V1, doi: 10.17632/n96ncsr5g4.1

3- PhishTank Available online: https://phishtank.org.


## Authors & Contributions
**Jawaher Alharbi**- Wrote the code, Resources, Data Curation, Methodology, Designed the software, Formal analysis, Project administration

**Manal Bayousef**- Methodology, Formal analysis, Supervision, Project administration

**Hind Almisbahi**- Designed the software, Formal analysis, Supervision, Project administration

## License
The code files and dataset are provided for research 
and reproducibility purposes only.

## Help/Contact 
For any questions or issues related to running 
the code, please contact **Jawaher Alharbi** at *jalharbi0086@stu.kau.edu.sa* 
