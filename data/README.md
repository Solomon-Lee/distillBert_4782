# Dataset Acquisition Guide

This repository uses the Hugging Face Datasets library to load common NLP benchmarks directly at runtime. No manual downloads or saves are required: datasets are fetched on demand and cached automatically.

## 1. Prerequisites

Make sure you have Python 3.x installed, then install:

```bash
pip install datasets
```

## 2. Loading Datasets

Simply call `load_dataset` with the dataset name (and config, if needed). Datasets are cached in the default Hugging Face cache directory (`~/.cache/huggingface/datasets`).

### Wikitext-2 Raw

```python
from datasets import load_dataset

ds = load_dataset(
    "wikitext",            # dataset repository
    "wikitext-2-raw-v1"    # specific config
)
# ds["train"], ds["validation"], ds["test"]
```

### IMDb (Sentiment Classification)

```python
from datasets import load_dataset

ds = load_dataset("imdb")
# ds["train"], ds["test"]
```

### SQuAD v1.1 (Question Answering)

```python
from datasets import load_dataset

raw_datasets = load_dataset("squad")
# raw_datasets["train"], raw_datasets["validation"]
```

### GLUE (General Language Understanding Evaluation)

```python
from datasets import load_dataset

# Replace 'sst2' with any GLUE task name or variable:
task_name = "sst2"
ds = load_dataset("glue", task_name)
# ds["train"], ds["validation"], ds["test"]
```

## 3. Colab Usage (Optional)

On Google Colab, after loading the dataset you can inspect or preprocess it in-place. If you need to export raw files, you can zip the default cache folder and download:

```bash
!zip -r datasets.zip ~/.cache/huggingface/datasets
```

```python
from google.colab import files
files.download("datasets.zip")
```

No extra saving steps are necessary unless you want to package the cache for reuse across sessions.

---

_Datasets provided by the Hugging Face Datasets library._
