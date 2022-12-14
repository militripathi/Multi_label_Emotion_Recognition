# GoEmotions

**GoEmotions** is a corpus of 58k carefully curated comments extracted from Reddit,
with human annotations to 27 emotion categories or Neutral.

* Number of examples: 58,009.
* Number of labels: 27 + Neutral.
* Maximum sequence length in training and evaluation datasets: 30.

On top of the raw data, we also include a version filtered based on reter-agreement, which contains a train/test/validation split:

* Size of training dataset: 43,410.
* Size of test dataset: 5,427.
* Size of validation dataset: 5,426.

The emotion categories are: _admiration, amusement, anger, annoyance, approval,
caring, confusion, curiosity, desire, disappointment, disapproval, disgust,
embarrassment, excitement, fear, gratitude, grief, joy, love, nervousness,
optimism, pride, realization, relief, remorse, sadness, surprise_.


This directory includes the data and code for data analysis scripts. We also
include code for our baseline model, which involves fine-tuning a pre-trained
[BERT-base model](https://github.com/google-research/bert).

For more details on the design and content of the dataset, please see our
[paper](https://arxiv.org/abs/2005.00547).

Refer to our [GoEmotions Model Card](goemotions_model_card.pdf) for recommended
uses of models built with this data, as well as considerations and limitations
relating to the GoEmotions data.



## Data

Data in the `data` folder. \

```

Our raw dataset, split into three csv files, includes all annotations as well as metadata on the comments. Each row represents a single rater's annotation for a single example. This file includes the following columns:

* `text`: The text of the comment (with masked tokens, as described in the paper).
* `id`: The unique id of the comment.
* `author`: The Reddit username of the comment's author.
* `subreddit`: The subreddit that the comment belongs to.
* `link_id`: The link id of the comment.
* `parent_id`: The parent id of the comment.
* `created_utc`: The timestamp of the comment.
* `rater_id`: The unique id of the annotator.
* `example_very_unclear`: Whether the annotator marked the example as being very unclear or difficult to label (in this case they did not choose any emotion labels).
* separate columns representing each of the emotion categories, with binary labels (0 or 1)

The data we used for training the models includes examples where there is agreement between at least 2 raters. Our data includes 43,410 training examples (`train.tsv`), 5426 dev examples (`dev.tsv`) and 5427 test examples (`test.tsv`). These files have _no header row_ and have the following columns:

1. text
2. comma-separated list of emotion ids (the ids are indexed based on the order of emotions in `emotions.txt`)
3. id of the comment



```

```


## Disclaimer
- We are aware that the dataset contains biases and is not representative of global diversity.
- We are aware that the dataset contains potentially problematic content.
- Potential biases in the data include: Inherent biases in Reddit and user base biases, the offensive/vulgar word lists used for data filtering, inherent or unconscious bias in assessment of offensive identity labels, annotators were all native English speakers from India. All these likely affect labelling, precision, and recall for a trained model.
- The emotion pilot model used for sentiment labeling, was trained on examples reviewed by the research team.
- Anyone using this dataset should be aware of these limitations of the dataset.
