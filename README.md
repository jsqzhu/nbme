# NBME - Score Clinical Patient Notes

## Background

## Objectives
An NER model to identify and map out feature entities in clinical notes

## Data
The provided train dataset is consisted of 10 distinct clinical cases, each with varying number of feature entities that needs to be mapped out. For each of the cases, 100 distinct notes (pn_num) are included that cover an average of X feature entities.  

## Approach
## I. Token classificaition
[Bio_ClinicalBert](https://huggingface.co/emilyalsentzer/Bio_ClinicalBERT) is a BERT-based model that is pre-trained on all notes from [MIMIC III](https://www.nature.com/articles/sdata201635) database. 
Training: convert clinical notes into word embedding for training using a pre-trained Bert Model; the target for prediction is masked clinical notes based on identified feature entities
## II. 
