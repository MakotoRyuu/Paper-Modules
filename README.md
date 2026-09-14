# Paper Modules

**本仓库仅收集模块代码，请自行使用AI工具进行调试**<br>
**本仓库仅收集模块代码，请自行使用AI工具进行调试**<br>
**本仓库仅收集模块代码，请自行使用AI工具进行调试**<br>

一个面向深度学习论文复现与模型开发的即插即用 PyTorch 模块库。

本仓库收集论文中常见且值得复用的网络组件，例如 ConvLSTM、各类注意力机制、特征融合模块、卷积块、归一化层和损失函数。每个模块都尽量保持独立、接口清晰，并附带论文出处、张量形状说明、最小示例和测试，方便直接嵌入自己的模型。

> GitHub About 描述：深度学习论文即插即用模块库：PyTorch 实现、论文出处、使用示例与测试。

## 为什么建立这个仓库？

阅读论文时，我们经常需要重复实现同一类组件；网上的实现又可能存在版本过旧、输入维度不明、缺少测试或偏离原论文等问题。本仓库希望提供一个轻量、可验证的模块集合，让研究者能够快速完成基线搭建、消融实验和结构组合。

## 目录结构

```text
paper-modules/
├── paper_modules/
│   ├── recurrent/          # ConvLSTM、ConvGRU 等
│   ├── attention/          # 注意力模块
│   ├── convolution/        # 卷积与多尺度模块
│   ├── fusion/             # 特征融合模块
│   ├── transformer/        # Transformer 组件
│   ├── normalization/      # 归一化与激活
│   ├── losses/             # 损失函数
│   └── sampling/           # 上采样与下采样
└── README.md
```

## 快速开始

项目完善后，可通过以下方式安装：

```bash
git clone https://github.com/OWNER/paper-modules.git
cd paper-modules
pip install -e .
```

示例：

```python
import torch
from paper_modules.recurrent import ConvLSTM

x = torch.randn(2, 10, 3, 64, 64)  # [batch, time, channels, height, width]
model = ConvLSTM(
    input_channels=3,
    hidden_channels=32,
    kernel_size=3,
    batch_first=True,
)

output, state = model(x)
print(output.shape)
```

以上导入接口是仓库的目标设计；相应模块实现加入后即可运行。
