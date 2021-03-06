# SQLNet

This repo provides an implementation of SQLNet and Seq2SQL neural networks for predicting SQL queries on [WikiSQL dataset](https://github.com/salesforce/WikiSQL). The paper is available at [here](https://arxiv.org/abs/1711.04436).

## Citation

> Xiaojun Xu, Chang Liu, Dawn Song. 2017. SQLNet: Generating Structured Queries from Natural Language Without Reinforcement Learning.

## Bibtex

## Installation
The data is in `data.tar.bz2`. download the data and Unzip the code by running
```bash
bash download_data.sh
```

The code is written using PyTorch in Python 2.7. Check [here](http://pytorch.org/) to install PyTorch. You can install other dependency by running 
```bash
pip install -r requirements.txt
```

## Downloading the glove embedding.
Download the pretrained glove embedding from [here](https://github.com/stanfordnlp/GloVe) using
```bash
bash download_glove.sh
```
## Extract the glove embedding for training.
Run the following command to process the pretrained glove embedding for training the word embedding:
```bash
python --extract_emb
```

## Train
The training script is `train.py`. To see the detailed parameters for running:
```bash
python --train -h
```

Some typical usage are listed as below:

Train a SQLNet model with column attention:
```bash
python --train --ca
```

Train a SQLNet model with column attention and trainable embedding (requires pretraining without training embedding, i.e., executing the command above):
```bash
python --train --ca --train_emb
```

Pretrain a [Seq2SQL model](https://arxiv.org/abs/1709.00103) on the re-splitted dataset
```bash
python --train --baseline --dataset 1
```

Train a Seq2SQL model with Reinforcement Learning after pretraining
```bash
python --train --baseline --dataset 1 --rl
```

## Test
The script for evaluation on the dev split and test split. The parameters for evaluation is roughly the same as the one used for training. For example, the commands for evaluating the models from above commands are:

Test a trained SQLNet model with column attention
```bash
python --test --ca
```

Test a trained SQLNet model with column attention and trainable embedding:
```bash
python --test --ca --train_emb
```

Test a trained [Seq2SQL model](https://arxiv.org/abs/1709.00103) withour RL on the re-splitted dataset
```bash
python --test --baseline --dataset 1
```

Test a trained Seq2SQL model with Reinforcement learning
```bash
python --test --baseline --dataset 1 --rl
```

## Inference mode
To run the script for evaluating and pretty printing output
```bash
python --evaluate --ca
```

Inference mode with a trained SQLNet model with column attention and trainable embedding:
```bash
python --evaluate --ca --train_emb
```

Inference mode with a trained [Seq2SQL model](https://arxiv.org/abs/1709.00103) withour RL on the re-splitted dataset
```bash
python --evaluate --baseline --dataset 1
```

Inference mode with a trained Seq2SQL model with Reinforcement learning
```bash
python --evaluate --baseline --dataset 1 --rl
```
