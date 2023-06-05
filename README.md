# Malware Behavior Labels
This repo contains the behavioral labels for the malware from the [Microsoft Malware Classification Challenge](https://arxiv.org/abs/1802.10135)
associated with the [2015 Kaggle competition](https://www.kaggle.com/c/malware-classification)
corresponding to the work in our [Mind the Gap: On Bridging the Semantic Gap between Machine Learning and Malware Analysis](https://dl.acm.org/doi/10.1145/3411508.3421373).
It also contains code for loading the data and the behavioral labels and basic examples for 
creating a behavioral-based classifier as outlined in our aforementioned work. 

If the data and/or code is used, please cite:
```
@inproceedings{10.1145/3411508.3421373,
author = {Smith, Michael R. and Johnson, Nicholas T. and Ingram, Joe B. and Carbajal, Armida J. and Haus, Bridget I. and Domschot, Eva and Ramyaa, Ramyaa and Lamb, Christopher C. and Verzi, Stephen J. and Kegelmeyer, W. Philip},
title = {Mind the Gap: On Bridging the Semantic Gap between Machine Learning and Malware Analysis},
year = {2020},
isbn = {9781450380942},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3411508.3421373},
doi = {10.1145/3411508.3421373},booktitle = {Proceedings of the 13th ACM Workshop on Artificial Intelligence and Security},
pages = {49–60},
numpages = {12},
location = {Virtual Event, USA},
series = {AISec'20}
}
```

## Data
The data that we provide **only** encompasses the behavioral labels. 
The data can be obtained at the [2015 Kaggle competition](https://www.kaggle.com/c/malware-classification)
website and will need to obtained first to run these experiments.

There are two versions of the behavioral labels in the data folder:
1. One version in excel format is what we used for generating the results from our paper.
2. The csv is our newer revised version.

The dataloaders have been updated to support both but the models shared only correspond to the old data.

This data set was chosen as it provides malware families and was highly cited. 
The behaviors were extracted through a manual process of reading threat reports 
and mapping the behaviors to the [Malware Behavior Catalog v1.1](https://github.com/MBCProject/mbc-markdown/tree/v1.1).
More details are provided in our paper.

## Code Examples
This repo provides the code to load the behavior labels and our baseline
experiments. See our paper for details about the chosen models.
As predicting behaviors (as opposed to intent--benign vs. malicious)
alters the challenge to multi-target (54 possible binary classes) from a binary
challenge, the code helps to provide a starting point for running more
experiments on the collected data.
All code is licensed is covered by the GNU Affero General Public
License version 3 (AGPL-v3). 

### Getting Started
* `conda create -n <choose your name> tensorflow-gpu`
  * We used Tensorflow 0.2.2 and CUDA 10.1
   * If using pytorch any python 3 conda environment will do
   * Provided `requirements.txt` for everything else

#### How to Train Baseline Model
* Select the following parameters to run trainer.py
  * `--num_epochs` number of epochs to train with
  * `--batch_size` number of batches to trian with
  * `--learning_rate` learning rate to train with
  * `--test_family` malware family to withhold for testing
  * Example: `python trainer.py --num_epochs 20 --batch_size 248 --learning_rate 0.001 --test_family gatak`

#### How to Test Baseline Model
* Select the following parameters to run tester.py
  * `--model` path to CNN model to test
  * `--batch_size` number of batches to test with
  * `--test_family` malware family to test model with
  * `--results_file` file to write test metrics to
  * Example: `python tester.py --model ./models/my_path.pth --batch_size 248 --test_family gatak --results_file ./results.pkl`

#### Different models
* Our transfer learning was built on a tensorflow model
  * See the malconv sub-directory for our approach to that

## Contacts
For questions regarding the experiments or the labels, please contact any of the authors of [our paper](https://dl.acm.org/doi/10.1145/3411508.3421373)