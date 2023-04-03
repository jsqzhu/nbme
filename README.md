# NBME - Score Clinical Patient Notes

## Background

## Objectives
An NER model to identify and map out feature entities in clinical notes

## Data
The provided train dataset is consisted of 10 distinct clinical cases, each with varying number of feature entities that needs to be mapped out. For each of the cases, 100 distinct notes (pn_num) are included that cover an average of X feature entities.  

## Approach
Two approaches for token classification
## I. NER using One Segment
In the first approach, note text is first tokenized; each token is then mapped to a total of 143 (features) + 1(empty) classes
Pre-trained models to consider:
[Bio_ClinicalBert](https://huggingface.co/emilyalsentzer/Bio_ClinicalBERT): a BERT-based model that is pre-trained on all notes from [MIMIC III](https://www.nature.com/articles/sdata201635) database; but the limitation is the max_sequence_length = 128
Roberta: OOM issue -> parralel computing or ??

## II. Two Segment
In the second approach, feature entities + note text are both fed into BERT as inputs; the resulting tokens are mapped to a total of 3 classes:
- 1: token is part of a feature entity
- -1: if token is part of the feature entity (seq_id=0), or if it belongs to a special tokens ([CLS], [SEP]) that are not part of the note text
- 0: (default) tokens from note text and not part of a feature entity

