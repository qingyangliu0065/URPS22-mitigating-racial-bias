# URPS22-mitigating-racial-bias

## Project Background Overview

This work is based on the problem proposed by [Obermeyer et al., 2019](https://gitlab.com/labsysmed/dissecting-bias) where a non-negligible racial bias embedded in a current wide-using prediction algorithm. 

In this paper *Dissecting racial bias in an algorithm used to manage the health of populations*, the authors focused on a live, scaled algorithm deployed nationwide and applied to roughly 200 million people in the United States. Based on the assumption that the treatment effect of a certain healthcare program is monotonic in the patient’s health risk level, this prediction algorithm aimed at identifying the top 3 percent of people with the greatest health risk to be automatically enrolled into the program, and also the top 45 percent people to be considered as candidates of enrollment.

Researcher argued that the usage of an artificial health risk score is problematic since there exist health disparities conditional on the risk score for two racial groups: White and Black. At the same level of algorithm-predicted risk, Blacks have significantly more illness burden than Whites. There are, however, few disparities in healthcare costs conditioned on predicted risk score.

The reason is inherent in how the prediction algorithm is designed. The algorithm takes in raw insurance claims data, such as demographics, insurance type, diagnosis and procedure codes, medications, and detailed costs. The chosen label is health costs per year instead of actual healthcare needs. The algorithm specifically excludes race. While this might make the algorithm seem unbiased, reality is a bit more complicated. Relevant literature suggests that Blacks on average generate lower costs than whites given similar health conditions due to various socioeconomic factors. This shows that costs per year and race are not independent variables, which suggests that the algorithm is trained on an inherently biased label.

The author suggests that a careful choice of label on which we train the prediction algorithm matters. By finding a less biased label, we can obtain less biased results. The author conducted experiments on the same dataset but with different labels, such as avoidable costs and active chronic conditions. Results of the experiments show that the predicted fraction of Blacks over the 97 percentile of risk score using active chronic conditions (26.7%) as the training label is the closest to the actual fraction, which is approximately 47%. This indicates that active chronic conditions is a less biased label compared with total cost and total avoidable cost. We should also notice that this result is far from an optimal solution, and it could be difficult to find or synthesize a label that minimizes racial bias. Therefore we tried to explore a more efficient approach to resolve this problem. 

## Core Method Introduction

The method that we are using is adapted from a paper by Heinrich Jiang and Ofir Nachum [Jiang & Nachum, 2020](https://github.com/google-research/google-research/tree/master/label_bias). The paper aims to explain why biases are embedded in certain machine learning algorithms and to correct the biases without changing the dataset. The core method assumes that a set of unknown and unbiased labels exists and is overwritten by a biased agent who intends to provide accurate labels. The goal of this method is to obtain an unbiased machine learning classifier by re-weighting the data points without changing the labels. We will discuss in our report that the re-weighting technique in this paper guarantees that training on the re-weighted dataset with the biased labels is equivalent to training with the unbiased labels that are unknown to us. We will also show in the experiment section that on our dataset this method gives a fairly good fairness-accuracy trade-off compared to the baseline models.

## Instruction for Reproducibility
### Dependencies
Python 3.9

### Code
The experiment implementation can be found in [Experiments.ipynb](Experiments.ipynb). Please make sure to have the corresponding data files under the `\Data` folder. 

## Results
Please see the project report [here](Project_Report.pdf). 
