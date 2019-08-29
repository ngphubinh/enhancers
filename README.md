# iEnhancer-ECNN: Identifying Enhancers and their Strength using Ensembles of Convolutional Neural Networks
Quang H. Nguyen, Thanh-Hoang Nguyen-Vo, Khanh Le, Trang T.T. Do, Susanto Rahardja and Binh P. Nguyen

## Introduction

Enhancers are non-coding DNA fragments which are crucial in gene regulation (e.g., transcription and translation). Due to the great difference in the locating site among these enhancers, identifying their locations is, therefore, more complicated than other genetic factors. To address this biological issue, several in silico studies have been done to identify and classify enhancer sequences among a myriad of DNA sequences using computational advances. Although recent studies have come up with improved performance, shortfalls in these learning models still remain. To overcome the current limitations of previous learning models, we introduce iEnhancer-ECNN - a novel prediction framework using One-Hot Encoding (OHE) for data transformation and ensemble Convolutional Neural Network (CNN) for model construction to identify enhancers as well as classify their strength. The dataset from Liu et al.'s study was used to develop and evaluate the models. Comparative analysis between iEnhancer-ECNN and other state-of-the-arts was done to fairly assess the model performance.

## Dataset

We re-used the dataset used in Liu et al.'s studies to fairly assess and compare the model performance between ours and the others. This dataset was also used in other studies addressing the same problems as ours. In this dataset, the information about enhancers in nine different cell lines was collected and the DNA sequences were extracted in the form of short fragments with the same length of 200bp. The CD-HIT was used to exclude the pairwise sequences whose similarities were more than 20\%.

The development dataset encompasses 1,484 enhancer samples (742 strong enhancer and 742 weak enhancer samples) and 1,484 non-enhancer samples. The independent test dataset contains 200 enhancers (100strong enhancers and 100 weak enhancers) and 200 non-enhancers. For model training, we first randomly divided the development dataset into five data folds (or parts), then performed the training process using a fixed ratio of the training set over the validation set of 4:1 with alternation. Finally, we combined the five trained deep learning models using an ensemble method then used the ensemble model to test on the independent test dataset (as in the Figure below). We repeated the whole process including data partitioning, model training and testing multiple times for a fair assessment of our model.

<img src="overview.svg?sanitize=true" width="800">

## CNN Architecture

The CNN architecture is described in the Figure below. The network input is a $200 \times 8$ matrix encoding a sequence with length 200. The network consists of six 1-D CNN blocks with Batch Normalization. Besides, for every three blocks of 1-D CNN, there is one 1-D Max Pooling layer. After the CNN and the Max Pooling layers, 768 features are obtained and fed into two Fully Connected Layers with 768 and 256 input neurons using the rectified linear unit (ReLU) and sigmoid activation functions, respectively, to produce a probability that the input sequence is an enhancer. The same architecture is used to classify strong enhancers and weak enhancers. The models were trained within 20 epochs using the binary cross entropy loss with Adam optimizer and the learning rate of $0.0001$. For each CNN model, the optimal network was selected corresponding to the epoch at which the loss on the validation set was minimal.

<img src="cnn.svg?sanitize=true" width="800">

## Results

Our results demonstrated that iEnhancer-ECNN has better performance compared to other state-of-the-art predictors. The accuracy of the ensembled training model for enhancer identification and classification are 0.765 and 0.695, respectively. In both enhancer identification and classification models, iEnhancer-ECNN achieves slightly lower specificity values compared to those of other methods introduced in previous studies. However, the improvement in the area under the receiver operating characteristics curve (AUC), sensitivity, and Matthews’s correlation coefficient (MCC) is remarkable, especially with respective to the enhancer classification model where the increases are about 13\%, 55.5\%, and 84\%, respectively.

## Download

- Data and code: [download](http://homepages.ecs.vuw.ac.nz/~nguyenb5/bioinformatics/enhancers/code_enhancers.zip)

## Contact

[Go to contact information](http://homepages.ecs.vuw.ac.nz/~nguyenb5/contact.html)
