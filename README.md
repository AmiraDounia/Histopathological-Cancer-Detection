# Histopathological-Cancer-Detection
Created an algorithm to identify metastatic cancer in small image patches taken from larger digital pathology scans. The data for this competition is a slightly modified version of the PatchCamelyon (PCam) benchmark dataset

## Motivation

* Clinical diagnosis of breast cancer is best achieved by a biopsy. The pathologist diagnose by manually examining the histology slides under the microscope. However, the traditional diagnosis system needs expertise and only experienced pathologists can accurately determine the tumor tissues.
* Currently, in various rural parts of India, people do not have access to good healthcare facilities. Also, new advanced equipment are not available in rural areas so it is even possible that patients are not diagnosed properly. One of the primary reasons for dismal healthcare in rural areas is shortage of experienced doctors.

## Dataset

The dataset used for the research is a slightly modified    version    of    the    PatchCamelyon    (PCam). The original PCam dataset contains duplicate images due to its probabilistic sampling, however, this   version   does   not   contain   duplicates.   The   dataset is open-source and can be downloaded from (<https://www.kaggle.com/c/histopathologic-cancer-detection/data>).   The   dataset   has   more   than   220K   RGB images  with  a  dimension  of  96x96x3.  The  given  problem  is  the  binary  classification  problem  where  the  associated label has two class labels i.e. tumor and non-tumor tissues. A  positive  label  indicates  that  the  center  32x32px  region  of a  patch  contains  at  least  one  pixel  of  tumor  tissue.

<img src="images/download (2).png" >

## Research Objectives

* Train various state-of-the-art deep learning architectures.
* Do a comparative study among the various models.
* Compare train-test splitting with stratified K-fold Cross-Validation.
* Apply image processing techniques such as Contrast Limited Adaptive Histogram Equalization (CLAHE).
* Apply various Image Augmentation techniques.
* Replace adaptive learning rate with one cycle policy(cyclic learning rate).
* Improve the model predictions with Test Time Augmentation(TTA).
* Measure the model performance on Accuracy, Precision, Recall, F1-measure and AUC ROC.

## Prerequisites

* Python (3.6)
* Keras (2.3.0)
* Tensorflow (2.1)
* NumPy (1.14.3)
* Sklearn (0.22.2)
* Albumentations (0.4.5)
* pandas (0.22.0)
* tqdm (4.19.8)
* opencv-python (3.4.2)


## How to Run Code

1. Git clone the repository to your local computer.
1. Download the data from [Kaggle](https://www.kaggle.com/c/histopathologic-cancer-detection/data).
1. Open a terminal in the folder containing the repository.
1. Run `python train_model.py` for training a model using hold-out train-validation split.
1. Run `python train_k_fold.py` training a model using stratified K-Fold cross validation split.
1. Run `python gradcam_vis.py` for visualizing the gradient class-activation maps.

#### `train_k_fold_tpu.py` can only run either on [Google Colab](https://colab.research.google.com/) or [GCP](https://console.cloud.google.com/) because TPUs are currently available on these online platforms.

## Methodology Flowchart

The figure below shows flowchart of our proposed methedology:

<img src="images/histopathology_flowchart.jpg" >

## Results Table
K-Fold result table of ```Model/baseline_model.py```:
| CNN Model | AUC-ROC |
| --------------- | --------------- |
| baseline_model with 4 Conv2D layers(w/o K-fold) | 0.9348 |
| baseline_model with 4 Conv2D layers(with 5-fold) | 0.9458 |
| baseline_model with 7 Conv2D layers(with 5-fold) | 0.9643 |
| baseline_model with 7 Conv2D layers(with 5x2-fold) | **0.9666** |

Comparative result of SOTA models based on Train-Validation split of 90-10\%:

| Architectures | Accuracy | Precision | Recall | F1-score | AUC-ROC |
| ----- | ----------- | ------------ | -------------- | --------------- | --------------- |
| DenseNet-169 | 0.98 | 0.98 | 0.98 | 0.98 | 0.9698 |
| DenseNet-201 | 0.97 | 0.97 | 0.97 | 0.97 | 0.9700 |
| SE-ResNet-50 | 0.968 | 0.97 | 0.97 | 0.97 | 0.9704 |
| Inception-V3 | 0.9693 | 0.97 | 0.97 | 0.97 | 0.9655 |
| SE-Inception-V3 | 0.9558 | 0.96 | 0.96 | 0.96 | 0.9681 |
| Inception-V3 + CBAM | 0.9656 | 0.97 | 0.97 | 0.97 | 0.9679 |
| Xception | 0.9821 | 0.98 | 0.98 | 0.98 | 0.9608 |
| OctaveResNet-50 | 0.959 | 0.96 | 0.96 | 0.96 | **0.9709** |

## Visualization

Following figure shows gradient class activation maps (Grad-CAM) on the penultimate convolutional block, which depict what areas of the image the CNN found most relevant for outcome
prediction. The heat map represents how important each region of the image is to the given classification. This
information can potentially be used by pathologists to make further hypotheses regarding the nature of the tumor.
<img src="images/grad_cam.png" >

## License

This repository is licensed under the terms of the MIT license.
