# Hugging Face
Let's have a quick look at the 🤗 Transformers library features. The library downloads pretrained models for Natural
Language Understanding (NLU) tasks, such as analyzing the sentiment of a text, and Natural Language Generation (NLG),
such as completing a prompt with new text or translating in another language.

First we will see how to easily leverage the pipeline API to quickly use those pretrained models at inference. Then, we
will dig a little bit more and see how the library gives you access to those models and helps you preprocess your data.

### Pipeline
The easiest way to use a pretrained model on a given task is to use `pipeline`. 🤗 Transformers
provides the following tasks out of the box:

- Sentiment analysis: is a text positive or negative?
- Text generation (in English): provide a prompt and the model will generate what follows.
- Name entity recognition (NER): in an input sentence, label each word with the entity it represents (person, place,
  etc.)
- Question answering: provide the model with some context and a question, extract the answer from the context.
- Filling masked text: given a text with masked words (e.g., replaced by `[MASK]`), fill the blanks.
- Summarization: generate a summary of a long text.
- Translation: translate a text in another language.
- Feature extraction: return a tensor representation of the text.

Let's see how this work for sentiment analysis (the other tasks are all covered in the [task summary](https://huggingface.co/transformers/task_summary.html)):

When typing this command for the first time, a pretrained model and its tokenizer are downloaded and cached. We will
look at both later on, but as an introduction the tokenizer's job is to preprocess the text for the model, which is
then responsible for making predictions. The pipeline groups all of that together, and post-process the predictions to
make them readable

You can see the second sentence has been classified as negative (it needs to be positive or negative) but its score is
fairly neutral.

By default, the model downloaded for this pipeline is called "distilbert-base-uncased-finetuned-sst-2-english". We can
look at its [model page](https://huggingface.co/distilbert-base-uncased-finetuned-sst-2-english) to get more
information about it. It uses the [DistilBERT architecture](https://huggingface.co/transformers/model_doc/distilbert.html) and has been fine-tuned on a
dataset called SST-2 for the sentiment analysis task.

Let's say we want to use another model; for instance, one that has been trained on French data. We can search through
the [model hub](https://huggingface.co/models) that gathers models pretrained on a lot of data by research labs, but
also community models (usually fine-tuned versions of those big models on a specific dataset). Applying the tags
"French" and "text-classification" gives back a suggestion "nlptown/bert-base-multilingual-uncased-sentiment". Let's
see how we can use it.

You can directly pass the name of the model to use to `pipeline`:


