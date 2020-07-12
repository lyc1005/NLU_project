# Find the Optimal Model for Covid-19 QA

![wordcloud](https://github.com/lyc1005/NLU_project/blob/master/image/covidalbert.png =100x100)
<img src="https://github.com/lyc1005/NLU_project/blob/master/image/covidalbert.png" width="48" height="48">

With the spread of COVID-19 and intensively accumulated research papers, it is important for researchers and users to efficiently get their questions answered. We would like to find out what are the optimal question and answering (QA) models in this specific do- main. Recently, BERT (Devlin et al., 2018) based models achieved the state-of-the-art results in multiple tasks including the QA task. And there are also domain specific BERT models existing, e.g., BioBert (Lee et al., 2019). Hence based on the ALBERT model (Lan et al., 2019), we build COVID-ALBERT, a COVID-19 specific model to explore whether it could help to improve the downstream QA task performance in this area. Finally, we compare the performance of 3 models: ALBERT, BioBert and COVID-ALBERT on our manually-labeled test Covid-19 QA dataset.

## Data

[CORD-19](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge): A resource of over 181,000 scholarly articles, including over 80,000 with full text, about COVID-19, SARS-CoV-2, and related coronaviruses.

[SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/): Stanford Question Answering Dataset (SQuAD) is a reading comprehension dataset, consisting of questions posed by crowdworkers on a set of Wikipedia articles, where the answer to every question is a segment of text, or span, from the corresponding reading passage, or the question might be unanswerable.

[BioASQ](http://bioasq.org/): BioASQ is a challenge on large-scale biomedical data semantic indexing and question answering.

[Covid-19 QA dataset](/COVID19_QA_testset.csv): This dataset was manually labelled by our team members and it contains question-answer pairs with the corresponding context sampled from CORD-19 articles.

![example](/image/example.png)

![answer_type](/image/answer type.png)

## Method

### Baseline model

1. ALBERT(https://arxiv.org/abs/1909.11942)

2. BioBERT(https://arxiv.org/abs/1901.08746)

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

![model_result](/image/model_result.png)

The performances for different models and different fine-tuning strategies on our manually labeled test set is shown in Table 1. We could see that the performances of ALBERT and BioBERT are similar and they both significantly outperform our pretrained COVID-ALBERT model.

The results in the table also show that fine-tuning on the BioASQ dataset harms the model’s performance no matter where we choose to use it.

![error_analysis](/image/error_analysis.png)

We use the prediction of ALBERT model (fine-tuned solely on SQuAD) that reaps the highest EM (exact match) to evaluate how well it could predict answers for different answer types. The result is showed at Table 2

## Contributors (names in alphabetical order)

Xiao Li (xl998@nyu.edu)

Yanyan Xu (yx2193@nyu.edu)

Yichen Liu (yl7043@nyu.edu)

Zian Chen (zc674@nyu.edu)

## Acknowledgments

* Thanks [Professor Sam Bowman](https://cims.nyu.edu/~sbowman/) for providing valuable advice and suggestion to this project.
* Thanks @techno246 and the codes our baseline model is based on.
* Thanks @wonjininfo and the codes for cleaning BioASQ datasets which we use for finetuning.

