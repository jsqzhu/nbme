# NBME - Score Clinical Patient Notes

## Background

## Objectives
An NER model to identify and map out feature entities in clinical notes

## Data
The provided train dataset is consisted of 10 distinct clinical cases, each with varying number of feature entities that needs to be mapped out. For each of the cases, 100 distinct notes (pn_num) are included that cover an average of X feature entities.  

## Approach
Two approaches for token classification
## I. NER using One Segment
In the first approach, note text is first tokenized; each token is then mapped to a total of 143 (features) + 1(empty) classes\
Pre-trained models considered:\
[Bio_ClinicalBert](https://huggingface.co/emilyalsentzer/Bio_ClinicalBERT): a BERT-based model that is pre-trained on all notes from [MIMIC III](https://www.nature.com/articles/sdata201635) database; but the limitation is the max_sequence_length = 128\
Roberta: OOM issue due to # of classes

## II. Two Segments
In the second approach, feature entities + note text are both fed into BERT as inputs; the resulting tokens are then mapped to a total of 3 classes:
- 1: token is part of a feature entity
- -1: if token is part of the feature entity (seq_id=0), or if it belongs to a special tokens ([CLS], [SEP]) that are not part of the note text
- 0: (default) tokens from note text and not part of a feature entity\

class = -1 is excluded from calculation of loss\

Pre-trained model considered:\
[PubMedBert](https://huggingface.co/microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract-fulltext): pretrained using data from PubMed\
Trained for 10 epochs using\
hyperparameters:

{
    "max_length": 416,\
    "padding": "max_length",\
    "return_offsets_mapping": True,\
    "truncation": "only_second",\
    "model_name": ("microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract-fulltext"),\
    "dropout": 0.2,\
    "lr": 1e-5,\
    "test_size": 0.2,\
    "valid_size":0.1,\
    "seed": 1268,\
    "batch_size": 8\
}

Model performance on test data:

{'Accuracy': 0.9941225458593618,\
  'precision': 0.7668322154523578,\
  'recall': 0.86587269468694,\
  'f1': 0.8133485391549908}

## Conclusions: model performs moderately well on test set but we did observe overfitting so there is room for improvement. Likely cause is the class imblance between class 1 and 0.
