# fake_news_classification_BERT
Trying to classify hyperpartisan/fake news from a labelled dataset of such using a BERT model

## Running the code
1. Open the code in google colab. 
2. Connect to your local runtime as per the instructions found [here](https://research.google.com/colaboratory/local-runtimes.html). Running it on the hosted runtime causes out of memory issues. 
3. Download the file `text.test.tsv` and save it in your working directory. (Alternatively, you can read the file directly from github, but in that case you will need to make slight changes to the notebook)
4. Run the code from google colab. 


# Details
Below are all relevant the implementation details

## Dataset
The dataset that has been used is the hyperpartisan news dataset found [here](https://zenodo.org/record/1489920). This dataset was created as part of this [task](https://www.aclweb.org/anthology/S19-2145/). This is a collection of two datasets, named by-article and by-publisher, consisting of news articles labelled whether they are hyperpartisan or not. I have only used the by-article dataset. 

## Preprocessing
For preprocessing, I have used the script provided by [the winning team](https://github.com/hyperpartisan-news-challenge/bertha-von-suttner/blob/master/Preprocessing/xml2line.py) for the [SemEval-2019 Task 4](https://pan.webis.de/semeval19/semeval19-web/). I have written some code to do some more preprocessing on the `.tsv` that is produced after running the above mentioned script.

## Model
I have used the distilBERT model found [here](https://huggingface.co/transformers/model_doc/distilbert.html). This is a lightweight version of the original BERT [model](https://github.com/google-research/bert) that is claimed to preserve 97% accuracy of the original BERT model. 

## Tokenization
The transformer distilBERT library lets users use the same tokenization technique that was originally mentioned in the paper that first proposed BERT or choose their own. I have stuck to the one originally proposed with BERT, i.e., WordPiece.

## Pretraining
I have used a pretrained model, `distilbert-base-uncased`, which is the distilBERT version of `bert-base-uncased` which in turn is the BERT model with all its weights, obtained from pretraining the model on a general English corpus (e.g. Wikipedia). 

## Hyperparameters
**Input sequence length:** The lenght of the input text sequence was truncated to the maximum length supported by the model, i.e., 512
**Padding:** Padding was used after tokenization to ensure all input sequence were of the same length
**Attention mask:** Mask was used to mask the padded parts

## Output layer
A logistic regression layer was used as the final layer to compute the probabilities. 

# Results
Pretrained weights | Title included | 1st run accuracy | 2nd run accuracy
-------------------|----------------|------------------|-----------------
distilbert-base-uncased | No | 76.5 | 75.9
distilbert-base-uncased | Yes | 74.1 | 79
distilbert-base-cased | No | 75.3 | 77.8
