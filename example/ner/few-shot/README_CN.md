## 快速上手

<p align="left">
    <b> <a href="https://github.com/zjunlp/DeepKE/blob/main/example/ner/few-shot/README.md">English</a> | 简体中文 </b>
</p>

### 环境依赖

> python == 3.8

- torch == 1.5
- transformers == 3.4.0
- deepke 

## 模型

<div align=center>
<img src="lightner-model.png" width="75%" height="75%" />
</div>

基于LightNER (COLING2022)的低资源实体识别方法 (详情请查阅论文 [https://arxiv.org/pdf/2109.00720.pdf](https://arxiv.org/pdf/2109.00720.pdf)).


### 克隆代码
```bash
git clone https://github.com/zjunlp/DeepKE.git
cd DeepKE/example/ner/few-shot
```
### 使用pip安装

首先创建python虚拟环境，再进入虚拟环境

- 安装依赖: ```pip install -r requirements.txt```

### 使用数据进行训练预测

- 存放数据： 可先下载数据 ```wget 120.27.214.45/Data/ner/few_shot/data.tar.gz```在此目录下

  在 `data` 文件夹下存放训练数据。包含CoNLL2003，MIT-movie, MIT-restaurant和ATIS等数据集。

- conll2003包含以下数据：

  - `train.txt`：存放训练数据集

  - `dev.txt`：存放验证数据集

  - `test.txt`：存放测试数据集

  - `indomain-train.txt`：存放in-domain数据集

- MIT-movie, MIT-restaurant和ATIS包含以下数据：

  - `k-shot-train.txt`：k=[10, 20, 50, 100, 200, 500]，存放训练数据集

  - `test.txt`：存放测试数据集


- 开始训练：模型加载和保存位置以及配置可以在conf文件夹中修改
  
  - 训练conll2003：` python run.py ` (训练所用到参数都在conf文件夹中，修改即可)

  - 进行few-shot训练：` python run.py +train=few_shot ` (若要加载模型，修改few_shot.yaml中的load_path)


- 每次训练的日志保存在 `logs` 文件夹内，模型结果保存目录可以自定义。
- 进行预测：在config.yaml中加入 - predict ， 再在predict.yaml中修改load_path为模型路径以及write_path为预测结果保存路径，再` python predict.py `

### 自定义Tokenizer

若您需要定制化自己的Tokenizer（例如`MBartTokenizer`用于多语言处理）。

您可在<a href="https://github.com/zjunlp/DeepKE/blob/main/src/deepke/name_entity_re/few_shot/module/datasets.py#L18">tokenizer</a>
中自定义分词器。

## 引用

如果您使用了上述代码，请您引用下列论文:

```bibtex
@article{DBLP:journals/corr/abs-2109-00720,
  author    = {Xiang Chen and
               Lei Li and
               Shumin Deng and
               Chuanqi Tan and
               Changliang Xu and
               Fei Huang and
               Luo Si and
               Huajun Chen and
               Ningyu Zhang},
  title     = {LightNER: {A} Lightweight Tuning Paradigm for Low-resource {NER} via
               Pluggable Prompting},
  journal   = {CoRR},
  volume    = {abs/2109.00720},
  year      = {2021},
  url       = {https://arxiv.org/abs/2109.00720},
  eprinttype = {arXiv},
  eprint    = {2109.00720},
  timestamp = {Thu, 01 Sep 2022 08:06:28 +0200},
  biburl    = {https://dblp.org/rec/journals/corr/abs-2109-00720.bib},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```

