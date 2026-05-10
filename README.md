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

