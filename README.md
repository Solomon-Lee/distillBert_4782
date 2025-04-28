# TinyDistilBERT: Re-implementing DistilBERT's Distillation Process

## Introduction

This GitHub repository contains a project that re-implements the distillation process from the paper _"DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter"_ by Sanh et al. (2019). The main contribution of the paper is creating a model that is significantly smaller and faster than BERT while retaining about 97% of its performance.

## Chosen Result

We aimed to replicate the results shown in Tables 1, 2, and 3 of the DistilBERT paper:

- **Table 1**: Performance retention on the GLUE benchmark.
- **Table 2**: Downstream task performance on IMDb and SQuAD v1.1.
- **Table 3**: Model size and inference speed gains.

These results are central to validating that distillation can trade off size and speed without major accuracy loss.

## GitHub Contents

- `code/`: Code for pretraining TinyDistilBERT on WikiText-2, fine-tuning notebooks for GLUE, IMDb, and SQuAD tasks, and a notebook for measuring inference time and model size.
- `data/`: Instructions on how to get the datasets needed for pretraining and finetuning.
- `poster/`: PDF file of our research poster that we made for reimplementing this paper.
- `report/`: PDF file of our 2 page report for this reimplementation.
- `results/`: Tables of our model results based on the benchmarks for GLUE, SQUaD, and IMDb.

## Re-implementation Details

We trained a smaller student model (TinyDistilBERT) using KL-divergence, masked language modeling (MLM) loss, and cosine embedding loss.

- **Teacher model**: BERT-base
- **Student model**: TinyDistilBERT
- **Pretraining dataset**: WikiText-2
- **Fine-tuning tasks**: GLUE benchmark, IMDb sentiment classification, and SQuAD v1.1
- **Challenges/Modifications**: Smaller dataset size led to lower generalization, especially on syntax-heavy tasks (e.g., CoLA, STS-B).

## Reproduction Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/Solomon-Lee/distillBert_4782.git
   cd distillBert_4782
   ```
2. Pretrain the student model by running through all the cells for DistillBert_training.ipynb
3. Fine-tune on downstream tasks with DistilBert_GLUE_CS4782.ipynb, DistilBert_IMDB_CS4782.ipynb, DistilBert_SQUAD_CS4782.ipynb, and DistilBert_Second_step_SQUAD_CS4782.ipynb.
4. Evaluate model size and inference speed on DistillBert_Inference_GLUE_CS4782.ipynb.

**Resources needed**:

- GPU (1 T4 GPU) for pretraining and fine-tuning.
- CPU for inference speed testing (optional).

## Results/Insights

- TinyDistilBERT retained ~70% of BERT's performance on GLUE tasks but struggled on CoLA and STS-B tasks.
- Achieved comparable performance on IMDb but struggled on SQuAD.
- Confirmed large reductions in model size and faster inference compared to BERT.
- Smaller pretraining corpus impacts syntax-heavy tasks more severely.

## Conclusion

This project validates that model distillation can significantly reduce computational costs while maintaining strong performance. Pretraining data size plays a crucial role in generalization, especially for complex tasks like QA as seen with the low benchmark scores on CoLA, STS-B, and SQuAD.

## References

- Sanh, Victor, et al. _“DistilBERT, a Distilled Version of BERT: Smaller, Faster, Cheaper and Lighter.”_ [arxiv.org/abs/1910.01108](https://arxiv.org/abs/1910.01108)
- [WikiText-2 Dataset](https://paperswithcode.com/dataset/wikitext-2)
- [GLUE Benchmark](https://gluebenchmark.com/)
- [IMDb Dataset](https://www.kaggle.com/datasets/hijest/genre-classification-dataset-imdb)
- [SQuAD Dataset](https://rajpurkar.github.io/SQuAD-explorer/)

## Acknowledgements

This project was completed as part of coursework for CS4782 (Deep Learning) at Cornell University. Thanks to the instructors and TAs for guidance and support during this project and the peer-reviewers for taking a look at our reimplementation work!
