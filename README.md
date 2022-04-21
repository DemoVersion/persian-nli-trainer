# Persian NLI Trainer

This repository is created with the aim to provide better models for NLI in persian, with the transparent codes for training I hope you guys find it inspiring and build better model in the future. for more details about the task and methods used for training check the [medium post](https://haddadhesam.medium.com/) and notebooks.


# Dataset

The dataset used for training is Wiki D/Similar dataset (wiki-d-similar.zip), obtained from [Sentence Transformers](https://github.com/m3hrdadfi/sentence-transformers) library.

# Model

The proposed model is published at HuggingFace Hub with the name of ``demoversion/bert-fa-base-uncased-haddad-wikinli``. You can download and use the model from [HuggingFace Website](https://huggingface.co/demoversion/bert-fa-base-uncased-haddad-wikinli) or directly in transformers library like this:

    from transformers import pipeline
    model = pipeline("zero-shot-classification", model="demoversion/bert-fa-base-uncased-haddad-wikinli")
    labels = ["ورزشی",
			    "سیاسی",
			    "علمی",
			    "فرهنگی"]
		template_str = "این یک متن {} است."
		str_sentence = "مرحله مقدماتی جام جهانی حاشیه‌های زیادی داشت."
		model(str_sentence, labels, hypothesis_template=template_str)
The result of this code snippet is:

    Asking to truncate to max_length but no maximum length is provided and the model has no predefined maximum length. Default to no truncation.
    {'labels': ['فرهنگی', 'علمی', 'سیاسی', 'ورزشی'],
     'scores': [0.25921085476875305,
       0.25713297724723816,
       0.24884170293807983,
       0.23481446504592896],
       'sequence': 'مرحله مقدماتی جام جهانی حاشیه\u200cهای زیادی داشت.'}
Yep, the right label (highest score) without training.
# Results

The result comparing to the orginal model published for this dataset is available in the table bellow.
|Model|dev_accuracy| dev_f1|test_accuracy|test_f1
|--|--|--|--|--|--|
|[m3hrdadfi/bert-fa-base-uncased-wikinli](https://huggingface.co/m3hrdadfi/bert-fa-base-uncased-wikinli)|77.88|77.57|76.64|75.99|
|[demoversion/bert-fa-base-uncased-haddad-wikinli](https://huggingface.co/demoversion/bert-fa-base-uncased-haddad-wikinli)|**78.62**|**79.74**|**77.04**|**78.56**|

# Notebooks
Notebooks used for training and evaluating is available bellow.
|            	| Notebook                                                                                                                                                                                    	|
|-----------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Training       	| [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DemoVersion/persian-nli-trainer/blob/main/notebooks/training.ipynb)       	|
| Evaluation               	| [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DemoVersion/persian-nli-trainer/blob/main/notebooks/evaluation.ipynb)               	|


