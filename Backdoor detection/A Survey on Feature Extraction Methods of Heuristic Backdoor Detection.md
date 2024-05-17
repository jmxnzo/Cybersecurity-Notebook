---
tags:
  - LiteratureNote
title: A Survey on Feature Extraction Methods of Heuristic Backdoor Detection
author(s): Zhimin Guo, Weijian Zhang, Wen Yang, Xin Che, Zheng Zhang and Mingyang Li
year: "2021"
date created: "{{date}}"
link: https://dl.acm.org/doi/fullHtml/10.1145/3474198.3478137
conference: ICFEICT 2021
usage: understanding pps only
---
## Backdoor detection methods
## signature-based methods
- create unique string of hash values for each file and match against a value stored in a database (malicious code hashes)
## behavioral-methods
- detect backdoor mutations, bcs the behaviour contains the same

## heuristical-methods
1. **Feature Extraction**: things like system calls made by the program, changes to system files or registry entries, network activity, file system modifications, memory usage patterns, and more
2. **Training a Classifier**: Once the features are extracted, they are used to train a classifier. A classifier is a machine learning algorithm that learns to distinguish between different classes of samples based on the provided features. In this case, the classifier is trained to distinguish between benign (safe) and malicious (potentially harmful) software based on the extracted features.
3. **Classification**: After the classifier is trained, it can be used to classify new samples. When a new file or program is encountered, its features are extracted, and the classifier predicts whether it is benign or malicious based on its learned knowledge from the training data. If the classifier identifies the sample as potentially malicious, appropriate actions can be taken, such as quarantining or blocking the file.

# Feature extraction methods
### static
- n-grams
- Printable Strings

- frequency of OpCodes:
	- Yewale et al. [[11](https://dl.acm.org/doi/fullHtml/10.1145/3474198.3478137#bib11)] proposed a new method to detect backdoors based on the frequency of op-codes in the portable executable file. They collected opcodes from 100 benign and backdoor files and found 20 most frequent opcodes, which could be used as feature vector for machine learning classifier. The success rate was about 96.67 percent.
- control flow graph 
	https://ieeexplore.ieee.org/document/6010676

- anti analysis
### dynamic 
- API calls
- 