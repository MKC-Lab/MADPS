# 基于对齐监督微调偏好学习的多智能体投放推送系统（Multi agent delivery push system based on alignment supervision fine-tuning preference learning）

提出了一种对齐监督微调偏好学习的多智能体投放推送系统框架，通过偏好学习对齐算法提升大模型表达的准确性，并将偏好学习对齐后的模型作为多智能体系统中的反思者用于提升大模型的推理能力，解决了投放系统未能充分利用用户精细偏好和上下文信息的问题，提升投放的准确性。

## 目录

- `LLaMA-Factory/`: 
    - `src/`: 对齐监督微调偏好学习对应的源代码文件夹。
- `MAS/`: 
    - `macrec/`: 源文件夹。
    - `config/`: 参数文件夹。
    - `data/`: 包含原始数据和预处理数据的数据集文件夹。
    - `scripts/`: 部分脚本文件夹。

## 偏好学习

1. 安装依赖

   克隆LLaMA-Factory并参照requirements.txt配置环境

   ```sh
   git clone https://github.com/hiyouga/LLaMA-Factory.git
   cd LLaMA-Factory
   conda create -n llamafactory
   conda activate llamafactory
   pip install -r requirements.txt
   ```

   将此仓库的`LLaMA-Factory/src/`替换对应位置的文件夹

2. 训练

   我们的训练方式与ORPO类似，在`examples/train_lora/llama3_lora_dpo.yaml`设定method中pref_loss为asft，使用下面命令进行训练

   ```sh
   llamafactory-cli train examples/train_lora/llama3_lora_dpo.yaml
   ```

## 多智能体投放推送

1. 安装依赖

   参照requirements.txt配置环境

   ```sh
   cd MAS
   conda create -n mas
   conda activate mas
   pip install -r requirements.txt
   ```

2. 评估

   修改`config/`中`api-config-example.json`的api内容，并修改reflect对应的地址为偏好学习后的模型地址

   参照`evaluate.sh`的示例脚本进行对应任务与数据集的评估

   