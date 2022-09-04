# Source-code Summarization
This repository contais all investigation data about source-code summarization techniques explored so far.

## Funcom

LeClair, A., Jiang, S., McMillan, C., "A Neural Model for Generating Natural Language Summaries of Program Subroutines", in Proc. of the 41st ACE/IEEE International Conference on Software Engineering (ICSE'19), Montreal, QC, Canada, May 25-31, 2019.
[Link to publication](https://arxiv.org/abs/1902.01954)

### Original repo
[Link to original repo](https://github.com/mcmillco/funcom)

### Source-code modifications
To be able to run training and predicting scripts on [Google Colab](https://colab.research.google.com), I have migrated the code from tensorflow 1.x to tensonflow 2.x. Apart from that, some properties were also not up to date with the provided data (Ex. 'dttrain' should be 'dtrain').

### Jupyter Notebook

[funcom.ipynb](https://colab.research.google.com/drive/18PP0Tz1ZGBA36ymXQ97opweQPqp5ul4P#scrollTo=D8hetAatfQYc)

```python
# Train data (just 1 epoch due to resources limitation)

%run '/content/drive/MyDrive/Doutorado/funcom/train.py' --model-type=attendgru --epochs=1 --gpu=0
```
```python
# Predict using generated model (.h5 file)

%run '/content/drive/MyDrive/Doutorado/funcom/predict.py' '/content/drive/MyDrive/Doutorado/funcom_scratch/data/outdir/models/attendgru_E01_1662135594.h5' --gpu=0
```
### Results

#### Example 1: 6314323
Prediction: `recalculate column and row count`

Reference:  `recalculates the column and row count considering all data`

Source-code (tokenized):
```java
private void recalculate column and row count column count 0 row count 0 for presented data data map data by id values change column and row count for data data
```

8868643
Prediction: <s> returns true if the given field is available </s>
Reference:  

4512280
Prediction: <s> checks if the current solution is a new solution </s>
Reference:

22622498
Prediction: <s> sets the debug flag </s>
Reference:

18925380
Prediction: <s> adds a new configuration to the file </s>
Reference: 
