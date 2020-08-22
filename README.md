# Find the Optimal Model for Covid-19 QA

<div align="center" >
<img src="https://github.com/lyc1005/NLU_project/blob/master/image/covidalbert.png" width="600" height="600">
</div>

With the spread of COVID-19 and intensively accumulated research papers, it is important for researchers and users to efficiently get their questions answered. We would like to find out what are the optimal question and answering (QA) models in this specific do- main. Recently, BERT (Devlin et al., 2018) based models achieved the state-of-the-art results in multiple tasks including the QA task. And there are also domain specific BERT models existing, e.g., BioBert (Lee et al., 2019). Hence based on the ALBERT model (Lan et al., 2019), we build COVID-ALBERT, a COVID-19 specific model to explore whether it could help to improve the downstream QA task performance in this area. Finally, we compare the performance of 3 models: ALBERT, BioBert and COVID-ALBERT on our manually-labeled test Covid-19 QA dataset.

## Data

[CORD-19](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge): A resource of over 181,000 scholarly articles, including over 80,000 with full text, about COVID-19, SARS-CoV-2, and related coronaviruses.

[SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/): Stanford Question Answering Dataset (SQuAD) is a reading comprehension dataset, consisting of questions posed by crowdworkers on a set of Wikipedia articles, where the answer to every question is a segment of text, or span, from the corresponding reading passage, or the question might be unanswerable.

[BioASQ](http://bioasq.org/): BioASQ is a challenge on large-scale biomedical data semantic indexing and question answering.

[Covid-19 QA dataset](/COVID19_QA_testset.csv): This dataset was manually labelled by our team members and it contains question-answer pairs with the corresponding context sampled from CORD-19 articles.

The following figure shows an example of question-answer pair with its context in the Covid-19 QA dataset.

<img src="https://github.com/lyc1005/NLU_project/blob/master/image/example.png" width="480" height="250">

The following figure shows the distribution of each answer type in the Covid-19 QA dataset.

<img src="https://github.com/lyc1005/NLU_project/blob/master/image/answer type.png" width="450" height="300">

## Method

### Baseline model

1. [ALBERT](https://arxiv.org/abs/1909.11942): ALBERT uses a very similar backbone architecture as BERT while it improve BERT by implementing factorized embedding parameters, cross-layer parameter sharing and inter-sentence coherence loss. The first two design choices provide the advantage of fewer parameters than BERT which enables faster training speed and less memory usage. The inter-sentence coherence loss enables ALBERT to change the next sentence prediction(NSP) task of BERT to a harder version - sentence-order prediction(SOP) which lets ALBERT achieve improvement on several down- stream tasks.

2. [BioBERT](https://arxiv.org/abs/1901.08746): BioBERT has focused on the biomedical domain. It significantly improves the performance on complex biomedical text mining tasks including biomedical named entity recognition, biomedical relation extraction, and biomedical question answering.

### Pre-training COVID-Albert

we choose to use ALBERT-base as our starting point and we then use the CORD-19 corpus to continue pre-training.

```
Data_processing.ipynb
```

### Fine-tuning the Models and Test on Our Custom QA Dataset

For fine-tuning the 3 models we choose, we use 3 different strategies:

1. Fine-tune the models solely on SQuAD.

2. Fine-tune the models firstly on SQuAD and then use BioASQ to do further fine-tuning.

3. Fine-tune the models firstly on BioASQ and then use SQuAD to do further fine-tuning.

After the fine-tuning is done, we then apply the models on our manually labeled COVID-19 QA dataset and use their performances as indicators on how well these models could generalize on larger COVID-19 QA tasks in the future.

```
Fine_tuning_for_Question_Answering.ipynb
```

## Results

<img src="https://github.com/lyc1005/NLU_project/blob/master/image/model_result.png" width="300" height="430">

The performances for different models and different fine-tuning strategies on our manually labeled test set is shown in Table 1. We could see that the performances of ALBERT and BioBERT are similar and they both significantly outperform our pretrained COVID-ALBERT model.

The results in the table also show that fine-tuning on the BioASQ dataset harms the model’s performance no matter where we choose to use it.

<img src="https://github.com/lyc1005/NLU_project/blob/master/image/error_analysis.png" width="400" height="240">

We use the prediction of ALBERT model (fine-tuned solely on SQuAD) that reaps the highest EM (exact match) to evaluate how well it could predict answers for different answer types. The result is showed at Table 2

## Discussion

Based on the results showed in previous section, we conclude that ALBERT is comprehensive enough for doing starter works at a new domain. We also want to point out that although our pretrained COVID-ALBERT performs the worst compared to ALBERT and BioBERT, it is still too early to determine that COVID-19 specific BERT model is not useful at all as the significant gap of F1/EM score between biomedical term answers and general term answer indicate those biomedical term requires better representation. The failure of COVID-ALBERT could be due to various design choices we make, different distribution in pre-training, fine-tuning and testing phases, or lack of computation power in pre_training. Hence in the future, when we have enough resources, we want to utilize larger text corpus and larger dupe factor to pretrain another more comprehensive COVID-19 BERT model and replicate our experiments in this work.

## Contributors (names in alphabetical order)

Xiao Li (xl998@nyu.edu)

Yanyan Xu (yx2193@nyu.edu)

Yichen Liu (yl7043@nyu.edu)

Zian Chen (zc674@nyu.edu)

## Acknowledgments

* Thanks [Professor Sam Bowman](https://cims.nyu.edu/~sbowman/) for providing valuable advice and suggestion to this project.
* Thanks @techno246 and the codes our baseline model is based on.
* Thanks @wonjininfo and the codes for cleaning BioASQ datasets which we use for finetuning.

