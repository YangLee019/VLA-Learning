# 第 3 阶段：OpenVLA

本阶段围绕一篇主论文组织为**三篇讲义**：先建立模型与训练主线，再看实验和适配，最后逐层拆解模型计算图与代码。目标是理解 OpenVLA 怎样在 RT-2 的“VLM 输出动作 token”路线中使用开放的模型与跨机器人数据，以及为什么下一阶段还需要重新设计动作输出和推理方式。

## 快速学习路线

| 顺序 | 建议用时 | 材料 | 核心问题 |
| --- | ---: | --- | --- |
| 1 | 40 分钟 | [模型、动作 token 与训练数据](./notes/01-模型与训练.md) | Prismatic、DINOv2/SigLIP、Llama 2 如何构成策略？动作为什么按分位数量化？ |
| 2 | 45 分钟 | [实验、微调与局限](./notes/02-实验与微调.md) | 16.5% 的胜出范围是什么？LoRA 和量化的计算口径是什么？ |
| 3 | 50 分钟 | [模型架构逐层拆解](./notes/03-模型架构逐层拆解.md) | 256 个视觉 token 如何进入 Llama？训练标签与推理 token 怎样对齐？ |
| 4 | 15 分钟 | 回到讲义末尾的自测，再核对下列原论文图表 | 能否分清 zero-shot、目标域微调和连续动作精度？ |

讲义按“先读中文、再核对论文”的方式撰写；示意图为本仓库重绘。外部网页均以**带说明文字的 Markdown 链接**放在相关论述处；这里集中给出固定入口。

## 原文与官方资源

| 资源 | 用途 |
| --- | --- |
| [OpenVLA 本地论文 PDF](./papers/OpenVLA_2406.09246v3.pdf) · [arXiv 版本页](https://arxiv.org/abs/2406.09246) · [论文 HTML v3](https://arxiv.org/html/2406.09246v3) | 主论文；优先核对 Fig. 2–6、Table 1–2、4、6–8，§3、§5–6 |
| [OpenVLA 项目页](https://openvla.github.io/) | 方法图、实验视频和资料入口 |
| [OpenVLA 官方代码仓库](https://github.com/openvla/openvla) | 检查点、推理、微调与数据加载示例；代码持续更新，注意与论文 v3 区分 |
| [融合视觉编码器实现](https://github.com/openvla/openvla/blob/main/prismatic/models/backbones/vision/dinosiglip_vit.py) · [HF 模型与投影器实现](https://github.com/openvla/openvla/blob/main/prismatic/extern/hf/modeling_prismatic.py) · [动作 tokenizer 实现](https://github.com/openvla/openvla/blob/main/prismatic/vla/action_tokenizer.py) | 配合架构讲义核对张量流和论文/代码表述差异 |
| [OpenVLA-7B 官方检查点](https://huggingface.co/openvla/openvla-7b) | 查询权重说明及推理接口；本仓库未复制权重 |

本地 PDF 为 **arXiv:2406.09246v3，37 页**；SHA-256 `353C37DF34458F12F969B14DFD8B77175B727B9CDDEA7BB891759BEDDEEFE1BE`。这里只保存论文，不下载大模型权重或完整 OXE 数据。

## 与前两阶段的连接

| 阶段 | 本阶段会继承或回答的问题 |
| --- | --- |
| [RT-2](../01-rt-series/notes/02-RT-2.md) | 把动作量化为 VLM 输出 token；OpenVLA 改用开放的 Prismatic/Llama 2 路线 |
| [OXE / RT-X](../02-cross-embodiment/notes/01-Open-X-Embodiment.md) | 从开放多机器人数据筛选训练混合；仍须辨别完整资源与实际训练子集 |
| [Octo](../02-cross-embodiment/notes/02-Octo.md) | 对照连续扩散动作块与离散单步动作、可微调接口 |
| 下一阶段 OpenVLA-OFT | 继续研究动作分块、连续输出与高频部署；本阶段先把原始 OpenVLA 的限制看清 |

## 完成标准

- 能从单张图像和语言指令画出 OpenVLA 的 7 维动作生成路径，写出其交叉熵目标与反量化步骤。
- 能解释 SigLIP、DINOv2、projector、Llama 2 的分工，以及机器人训练与互联网预训练的先后关系。
- 能指出 OpenVLA 训练集 97 万轨迹与 OXE 完整资源、Octo 80 万、RT-2-X 35 万的不同口径。
- 能按 WidowX、Google Robot、Franka 微调、LIBERO 四组实验分别陈述证据与边界。
- 能说明论文 Table 1–2 的 LoRA/量化测试使用模型变体，且控制频率会影响在线成功率。
