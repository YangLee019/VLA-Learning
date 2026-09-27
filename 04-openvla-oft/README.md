# 第 4 阶段：OpenVLA-OFT——动作分块、并行解码与连续控制

本阶段聚焦 **Fine-Tuning Vision-Language-Action Models: Optimizing Speed and Success**。问题是：已有 OpenVLA 具备跨数据集预训练表征，但沿用七个离散动作 token 的自回归生成，目标域微调后仍不易满足高频控制。OFT 研究的是**怎样微调现成 VLA**；它没有重新从零预训练 OpenVLA。[论文摘要与 §I](https://arxiv.org/html/2502.19645)

## 推荐学习顺序

| 顺序 | 建议用时 | 讲义 | 学习目标 |
| --- | ---: | --- | --- |
| 预备 | 15 分钟 | [OpenVLA 模型架构逐层拆解](../03-openvla/notes/03-模型架构逐层拆解.md) | 复习视觉前缀、因果自回归和动作 token |
| 1 | 60 分钟 | [OFT 架构与训练目标](./notes/01-OFT架构与训练目标.md) | 会画出平行输出 $K\times D$ 个连续动作的计算图 |
| 2 | 55 分钟 | [消融实验、部署与研究判断](./notes/02-消融实验与部署.md) | 会读成功率/吞吐/延迟口径，理解 FiLM 与局限 |
| 复盘 | 15 分钟 | 两篇讲义末尾的问题，核对论文 Fig. 2、Table I–III、附录 A | 能解释为何 26× 吞吐不等于 26× 更快闭环反馈 |

## 论文与官方入口

| 资源 | 用途 |
| --- | --- |
| [本地 OpenVLA-OFT PDF](./papers/OpenVLA-OFT_2502.19645v2.pdf) · [arXiv v2 HTML](https://arxiv.org/html/2502.19645) · [arXiv 版本页](https://arxiv.org/abs/2502.19645) | 主论文，重点 §III–VI 与附录 A |
| [项目主页](https://openvla-oft.github.io/) | 方法图、机器人视频与补充说明 |
| [官方代码](https://github.com/moojink/openvla-oft) | 推理示例、训练脚本、LIBERO/ALOHA 指南 |
| [训练脚本](https://github.com/moojink/openvla-oft/blob/main/vla-scripts/finetune.py) · [连续动作头](https://github.com/moojink/openvla-oft/blob/main/prismatic/models/action_heads.py) · [HF 模型](https://github.com/moojink/openvla-oft/blob/main/prismatic/extern/hf/modeling_prismatic.py) | 核对空动作位置、隐藏态、回归头与推理路径；代码会更新，复现须固定提交 |

本地 PDF 使用 **arXiv:2502.19645v2，24 页**；SHA-256 `B860AA1206B6CFB0CE8BE177F961379DD6A133D52CC74AC346636E0F4952A596`。这里保存论文与中文讲义，不复制模型权重或 LIBERO/ALOHA 数据。论文数字只在原文指定的硬件、数据、输入与评测条件下成立。

## 学完应能回答

1. 原版 OpenVLA 的七次串行生成怎样变成 OFT 的单次前向？双向注意力和空动作 embeddings 分别起何作用？
2. 为什么 $K=8$ 的吞吐可大幅提升，但一个 chunk 内的机器人仍然缺少新视觉反馈？
3. 离散 CE、连续 L1 和扩散分别对条件动作分布作了什么假设，实验能支持到什么程度？
4. 多视角和机器人状态怎样进入 Llama 序列？为何 ALOHA 上还需要 FiLM？
5. 97.1% 与 76.5% 的差异包含了哪些同时变化的条件，怎样用中间消融归因？
