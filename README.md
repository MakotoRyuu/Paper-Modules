# Paper Modules

**简体中文** | [English](#english)

一个面向深度学习论文复现与模型开发的即插即用 PyTorch 模块库。

本仓库收集论文中常见且值得复用的网络组件，例如 ConvLSTM、各类注意力机制、特征融合模块、卷积块、归一化层和损失函数。每个模块都尽量保持独立、接口清晰，并附带论文出处、张量形状说明、最小示例和测试，方便直接嵌入自己的模型。

> GitHub About 描述：深度学习论文即插即用模块库：PyTorch 实现、论文出处、使用示例与测试。

## 为什么建立这个仓库？

阅读论文时，我们经常需要重复实现同一类组件；网上的实现又可能存在版本过旧、输入维度不明、缺少测试或偏离原论文等问题。本仓库希望提供一个轻量、可验证的模块集合，让研究者能够快速完成基线搭建、消融实验和结构组合。

## 计划收录

| 分类 | 示例 |
| --- | --- |
| 时空建模 | ConvLSTM、ConvGRU、PredRNN 单元 |
| 注意力机制 | SE、CBAM、ECA、Non-local、Self-Attention、Cross-Attention |
| Transformer 组件 | Multi-Head Attention、位置编码、FFN、Patch Embedding |
| 卷积与多尺度 | Depthwise Separable Conv、ASPP、SPP、Deformable Conv |
| 特征融合 | FPN、BiFPN、门控融合、跨尺度融合 |
| 归一化与激活 | LayerNorm、RMSNorm、GroupNorm、Swish、GELU |
| 损失函数 | Focal Loss、Dice Loss、IoU Loss、Contrastive Loss |
| 上下采样 | PixelShuffle、可学习上采样、抗混叠下采样 |

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
├── examples/               # 最小运行示例
├── tests/                  # 单元测试
├── docs/                   # 公式、结构图与复现说明
├── CONTRIBUTING.md
├── CITATION.cff
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

## 每个模块应包含

- 原论文标题、作者、会议或期刊、年份及 DOI/arXiv 链接；
- 对原论文公式或结构的简要说明；
- 输入和输出的张量形状；
- 构造参数、默认值和适用场景；
- 可直接运行的最小示例；
- 前向传播、形状和梯度测试；
- 与原论文或官方实现存在的差异；
- 参数量、计算量或性能提示（适用时）；
- 原论文和参考实现的许可证信息。

## 设计约定

- 默认使用 PyTorch，张量布局必须在文档中明确标注。
- 模块应能单独导入，避免依赖完整训练框架。
- 默认参数尽量与原论文保持一致；差异必须明确说明。
- 不宣称“官方实现”，除非代码确实来自论文作者并获得相应许可。
- 数值结果无法完全复现时，应记录环境、随机种子和可能原因。
- 同一模块的改进版本应独立命名，避免覆盖原始实现。

## 模块状态

- `verified`：已与论文或官方实现核对，并通过测试。
- `implemented`：实现与基础测试完成，尚未充分对照验证。
- `experimental`：实验性实现，接口或行为可能改变。
- `deprecated`：不再建议使用，并提供替代方案。

## 路线图

- [ ] ConvLSTM
- [ ] SE Attention
- [ ] CBAM
- [ ] ECA Attention
- [ ] Non-local Block
- [ ] Multi-Head Self-Attention
- [ ] Focal Loss 与 Dice Loss
- [ ] 自动化测试与代码风格检查
- [ ] 模块索引和论文索引

## 贡献与引用

欢迎提交新的论文模块、测试、复现修正和文档改进。请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)，并使用 [MODULE_TEMPLATE.md](MODULE_TEMPLATE.md) 补全模块信息。

使用具体模块时，请优先引用其对应的原始论文。如果本仓库也对你的工作有帮助，可使用 [CITATION.cff](CITATION.cff) 引用本项目。

## 许可证

本仓库默认使用 [MIT License](LICENSE)。从其他项目改编的实现必须确认许可证兼容性，并在模块文档中注明来源。论文可公开阅读不代表其代码可以无条件复制。

---

<a id="english"></a>

# Paper Modules (English)

[简体中文](#paper-modules) | **English**

A plug-and-play PyTorch module library for reproducing deep learning papers and building research models.

This repository collects reusable neural-network components commonly found in papers, including ConvLSTM, attention mechanisms, feature-fusion blocks, convolutional blocks, normalization layers, and loss functions. Each module is designed to be self-contained and accompanied by its paper reference, tensor-shape documentation, a minimal example, and tests.

> GitHub About: Plug-and-play PyTorch modules from deep learning papers, with references, examples, and tests.

## Motivation

Researchers often reimplement the same building blocks when reading papers. Existing implementations may be outdated, undocumented, untested, or inconsistent with the original publication. This project provides a lightweight and verifiable collection for building baselines, running ablations, and combining architectures quickly.

## Planned categories

| Category | Examples |
| --- | --- |
| Spatiotemporal modeling | ConvLSTM, ConvGRU, PredRNN cells |
| Attention | SE, CBAM, ECA, Non-local, Self-Attention, Cross-Attention |
| Transformer components | Multi-Head Attention, positional encoding, FFN, Patch Embedding |
| Convolution and multi-scale | Depthwise Separable Conv, ASPP, SPP, Deformable Conv |
| Feature fusion | FPN, BiFPN, gated fusion, cross-scale fusion |
| Normalization and activation | LayerNorm, RMSNorm, GroupNorm, Swish, GELU |
| Losses | Focal Loss, Dice Loss, IoU Loss, Contrastive Loss |
| Sampling | PixelShuffle, learnable upsampling, anti-aliased downsampling |

## Repository structure

```text
paper-modules/
├── paper_modules/
│   ├── recurrent/
│   ├── attention/
│   ├── convolution/
│   ├── fusion/
│   ├── transformer/
│   ├── normalization/
│   ├── losses/
│   └── sampling/
├── examples/
├── tests/
├── docs/
├── CONTRIBUTING.md
├── CITATION.cff
└── README.md
```

## Quick start

Once the initial modules are implemented:

```bash
git clone https://github.com/OWNER/paper-modules.git
cd paper-modules
pip install -e .
```

Example:

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

The import above represents the intended public API and will become runnable when the corresponding implementation is added.

## Module requirements

Every module should include:

- the paper title, authors, venue, year, and DOI/arXiv link;
- a concise explanation of the relevant equations or architecture;
- input and output tensor shapes;
- constructor arguments, defaults, and intended use cases;
- a minimal runnable example;
- forward-pass, shape, and gradient tests;
- documented differences from the paper or official implementation;
- parameter-count, computational-cost, or performance notes when relevant;
- license information for the paper and reference implementation.

## Conventions

- PyTorch is the default framework, and tensor layouts must be documented.
- Modules should be independently importable without a full training framework.
- Defaults should follow the original paper whenever practical; differences must be explicit.
- Do not label an implementation “official” unless it comes from the authors and its license permits reuse.
- When exact numerical reproduction is not possible, record the environment, random seed, and likely causes.
- Improved variants should use distinct names rather than silently replacing the original implementation.

## Module status

- `verified`: checked against the paper or official implementation and covered by tests.
- `implemented`: implementation and basic tests are complete, but validation is limited.
- `experimental`: behavior or API may change.
- `deprecated`: no longer recommended; an alternative is provided.

## Roadmap

- [ ] ConvLSTM
- [ ] SE Attention
- [ ] CBAM
- [ ] ECA Attention
- [ ] Non-local Block
- [ ] Multi-Head Self-Attention
- [ ] Focal Loss and Dice Loss
- [ ] Automated tests and code-quality checks
- [ ] Module and paper indexes

## Contributing and citation

Contributions of paper modules, tests, reproduction fixes, and documentation are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) and use [MODULE_TEMPLATE.md](MODULE_TEMPLATE.md) to document a new module.

When using a module, cite its original paper first. If this repository also supports your work, cite the project using [CITATION.cff](CITATION.cff).

## License

The repository uses the [MIT License](LICENSE) by default. Adapted implementations must have compatible licenses and clearly identify their sources. Public access to a paper does not imply unrestricted permission to copy its code.
