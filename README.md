# COVIDBert: A Pre-trained Language Model for COVID-19 research papers

![wordcloud](/image/covidalbert.png)

With the spread of COVID-19 and intensively accumulated research papers, it is important for researchers and users to efficiently get their questions answered. We would like to find out what are the optimal question and answering (QA) models in this specific do- main. Recently, BERT (Devlin et al., 2018) based models achieved the state-of-the-art results in multiple tasks including the QA task. And there are also domain specific BERT models existing, e.g., BioBert (Lee et al., 2019). Hence based on the ALBERT model (Lan et al., 2019), we build COVID-ALBERT, a COVID-19 specific model to explore whether it could help to improve the downstream QA task performance in this area. Finally, we compare the performance of 3 models: ALBERT, BioBert and COVID-ALBERT on our manually-labeled test Covid-19 QA dataset.

## Data

[CORD-19](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge): A resource of over 181,000 scholarly articles, including over 80,000 with full text, about COVID-19, SARS-CoV-2, and related coronaviruses.

[SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/): Stanford Question Answering Dataset (SQuAD) is a reading comprehension dataset, consisting of questions posed by crowdworkers on a set of Wikipedia articles, where the answer to every question is a segment of text, or span, from the corresponding reading passage, or the question might be unanswerable.

[BioASQ](http://bioasq.org/): BioASQ is a challenge on large-scale biomedical data semantic indexing and question answering.

[Covid-19 QA dataset](/COVID19_QA_testset.csv)

## Method

We  use  Albert and  SQuad v2.0 dataset to get the baseline result. The baseline model can be run on

```
Question_Answering_with_ALBERT.ipynb
albert_fine_tune.txt
```

### pre-training COVIDBert

To process the COVID-19 corpora into the format suitable for pre-traing and a sample pretraining usage on Goole Cloud, we run the following notebook.

```
Data_processing.ipynb
```



## Acknowledgments

* Thanks for @techno246 and the codes our baseline model is based on.
* Thanks for @wonjininfo and the codes for cleaning BioASQ datasets which we use for finetuning.

