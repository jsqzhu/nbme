# NBME - Score Clinical Patient Notes

## Background

## Objectives
An NER model to identify and map out feature entities in clinical notes

## Data
Train dataset has 10 distinct clinical cases, each with varying number of feature entities that needs to be mapped out. For each of the cases, 100 distinct notes (pn_num) are included that cover an average of X feature entities.  

## Model
Training: convert clinical notes into word embedding for training using a pre-trained Bert Model; the target for prediction is masked clinical notes based on identified feature entities
