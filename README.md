# Woodpecker: 多模态大语言模型的幻觉修正

<p align="center">
    <img src="./assets/woodpecker.png" width="75%" height="75%">
</p>


<font size=7><div align='center' > :grapes: \[[阅读arXiv论文](https://arxiv.org/pdf/2310.16045.pdf)\] &nbsp; :apple: \[[我们的DEMO](https://deb6a97bae6fab67ae.gradio.live/)\] </div></font>

-----------------

下面将简要介绍本代码使用方法，原README文件在[这里](./README_original.md)

## 🛠️ 准备工作

1. 创建 conda 环境

```bash
conda create -n corrector python=3.10
conda activate corrector
pip install -r requirements.txt
```

2. 安装必要库和模型

-  请按照[链接](https://github.com/explosion/spaCy)说明安装 `spacy` 和相关模型库（用于一些文本处理操作）

```bash
pip install -U spacy
python -m spacy download en_core_web_lg
python -m spacy download en_core_web_md
python -m spacy download en_core_web_sm
```
- 对于我们的 **开放集检测器**， 请按照[链接](https://github.com/IDEA-Research/GroundingDINO)说明安装GroundingDINO

## ⭐ 使用

**1. 推理**

要基于图像和MLLM的输出文本进行修正，请运行下面的代码：

```Shell
python inference.py \
        --image-path {path/to/image} \
        --query "Some query.(e.x. Describe this image.)" \
        --text "Some text to be corrected." \
        --detector-config "path/to/GroundingDINO_SwinT_OGC.py" \
        --detector-model "path/to/groundingdino_swint_ogc.pth" \
        --api-key "sk-xxxxxxx" \

```
输出文本将打印在终端，中间结果将默认保存在 ```./intermediate_view.json```中。

***

**2. 建立Demo**

我们使用 mPLUG-Owl 作为默认MLLM进行实验。如果你想要复制在线DEMO，请克隆 [此项目](https://github.com/X-PLUG/mPLUG-Owl) 并在 https://github.com/BradyFU/Woodpecker/blob/e3fcac307cc5ff5a3dc079d9a94b924ebcdc2531/gradio_demo.py#L7 和  https://github.com/BradyFU/Woodpecker/blob/e3fcac307cc5ff5a3dc079d9a94b924ebcdc2531/gradio_demo.py#L35-L36 修改相关变量

运行下面的指令即可：

```bash
CUDA_VISIBLE_DEVICES=0,1 python gradio_demo.py
```
这里我们将修正器组件置于编号为0的 GPU 上， mPLUG-Owl 置于编号为1的GPU上。

## 📑 引用

```
@article{yin2024woodpecker,
  title={Woodpecker: Hallucination correction for multimodal large language models},
  author={Yin, Shukang and Fu, Chaoyou and Zhao, Sirui and Xu, Tong and Wang, Hao and Sui, Dianbo and Shen, Yunhang and Li, Ke and Sun, Xing and Chen, Enhong},
  journal={Science China Information Sciences},
  volume={67},
  number={12},
  pages={220105},
  year={2024},
  publisher={Springer}
}
```

