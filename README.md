# A Lightweight Content-Based Phishing Detection Approach Using Cross-Model Knowledge Distillation
This repository This repository contains the source code and dataset used in the manuscript: A Lightweight Content-Based Phishing Detection Approach Using Cross-Model Knowledge Distillation
# Abstract
Website phishing attacks present a complex security challenge, as the difficulty lies in distinguishing legitimate websites from phishing ones.
Despite the efforts of researchers to prevent phishing website attacks, current approaches still suffer from several major shortcomings, including:

- High computational cost.
- Lack of specialized web content analysis.
- Language-dependent detection limits generalizability.
- Features requiring third-party intervention.
- Limited analysis of the obfuscated JavaScript features.

To address these limitations, we propose the following contributions:

1- We constructed a realistic dataset derived from publicly available phishing and legitimate websites, enriched with features independent of language and third-party services. This dataset contains 32 content-based features, including those that indicate JavaScript obfuscation derived from the structure of JavaScript code that has been statically parsed. We extracted these features from Hypertext Markup Language (HTML) structures, embedded JavaScript elements, and external JavaScript files directly from target sites using static parsing. 

2- We apply knowledge distillation from a tree-based model (XGBoost) to a neural network model (MLP) for web content analysis, which is a promising approach that has received limited attention in previous studies. This approach leverages the complementary strengths of both architectures to improve generalizability and bridge their individual performance gaps in phishing website detection.

3- Our experiments show that the proposed approach demonstrates a balance between accuracy and speed at low computational cost.

# Dataset Information 

### Data Collection & Data Pre-processing: 
The dataset used in this study was collected from multiple sources. Legitimate URL data was obtained from publicly available datasets (e.g., [Kaggle](https://www.kaggle.com/datasets/bpmtips/46-million-domain-names-with-size-common-crawl) and [Mendeley Data)](https://doi.org/10.17632/n96ncsr5g4.1) , while phishing URLs were collected using the [PhishTank](https://phishtank.org) API. The API provides JSON reports of URLs, including both verified and unverified entries. Only URLs confirmed as live and verified phishing were retained. For phishing samples, web content was extracted using an API key in batches. Similarly, legitimate samples were also processed in batches. This approach was adopted to manage computational resources efficiently and to avoid interruptions or failures due to large volumes of requests. 

The collected data was then aggregated into a unified dataset. After feature extraction, the dataset contained:

- Legitimate dataset: 30,560 URLs
- Phishing dataset: 30,368 URLs

Data pre-processing steps (such as duplicate removal and handling missing values) and feature engineering, specifically feature selection, were applied. As a result, **a final dataset of 23,105 samples with 32 static content-based features was used for training and evaluation**. The labels are defined as: *Legitimate website = 0, Phishing website = 1*

