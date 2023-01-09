# Paper summary

## Task

Conversation answer selection aims to select an answer from candidate answers to satisfy the users' information need. 

## Model

![](.\img\Method.png)

Architecture of our proposed intent-calibrated self-training (ICAST) framework. The dashed and solid line represent the workflow of teacher model and student model. The blue and green solid line represent intent-aware and context-aware workflow, respectively. The intent-calibrated pseudo labeling module estimates intent confidence gain to select samples with high-quality intent labels, and calibrates the answer labels by incorporating selected intent labels as an extra input for answer selection.

# Running

## Requirements

```
Python == 3.9
Pytorch == 1.12.0
apex == 0.1
transformers == 4.17.0
```



## Datasets

1. We use [MSDIALOG](https://share.weiyun.com/JezuHlHU) and [MANTIS](https://share.weiyun.com/1ezb9Srg) datasets for training and test. 
2. After downloading the datasets, please place the MSDIALOG/teacher into teacher/msdialog/datasets, place the MSDIALOG/student into student/msdialog/datasets, place the MANTIS/teacher into teacher/mantis/datasets and place the MANTIS/student into student/mantis/datasets. 
3. Please download the pre-trained model [BERT-base-uncased](https://huggingface.co/bert-base-uncased) into prev_trained_model/bert-base-uncased. 

## Training and testing

#### Training the teacher model

```
## MSDIALOG dataset

cd student/msdialog
# Training
bash scripts/run_training.sh
# Testing
bash scripts/run_testing.sh
```

```
## MANTIS dataset

cd student/mantis
# Training
bash scripts/run_training.sh
# Testing
bash scripts/run_testing.sh
```



#### Training the student model

```
## MSDIALOG dataset

cd student/msdialog
# Training
bash scripts/run_training.sh
# Testing
bash scripts/run_testing.sh
```

```
## MANTIS dataset

cd student/mantis
# Training
bash scripts/run_training.sh
# Testing
bash scripts/run_testing.sh
```

To use our codes, train the teacher model first and select best teacher model on the development sets. After that,  put the checkpoint of teacher model into the folder of pre-trained model. Finally, train the student model with labeled and unlabeled dataset and select the best student model on the development set. 