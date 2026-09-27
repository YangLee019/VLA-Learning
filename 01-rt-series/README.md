# 第 1 阶段：从 RT-1 到 RT-2

**核心问题：**机器人策略如何从“为一个任务学动作”走向“理解语言、共享多任务经验，并借助视觉语言预训练处理新语义”？本阶段以 RT-1 和 RT-2 为主线。它们都把连续控制量离散化，但模型容量、预训练来源与动作输出接口不同。

## 时间紧时的阅读顺序

| 用时 | 内容 | 读完应能回答 |
| --- | --- | --- |
| 15 分钟 | [过渡讲义](./notes/00-从动作策略到语言条件.md) | 语言条件、语义泛化、动作泛化分别是什么？ |
| 35 分钟 | [RT-1 精读](./notes/01-RT-1.md) | 图像与语言如何变成动作？为什么设计 TokenLearner？ |
| 35 分钟 | [RT-2 精读](./notes/02-RT-2.md) | 为什么把动作写成 token？联合训练怎样迁移网页知识？ |
| 20 分钟 | [对照、自测与研究问题](./notes/03-对照与自测.md) | 哪些实验支持迁移，哪些能力仍受机器人数据限制？ |

先读讲义，再用下面标出的原论文图表核对。图中的流程为本仓库重绘的概念示意，不是原论文图片。

## 原论文

| 文件 | 版本与来源 | 优先核对 |
| --- | --- | --- |
| [RT-1 PDF](./papers/RT-1_2212.06817v2.pdf) | Brohan et al., *RT-1: Robotics Transformer for Real-World Control at Scale*，arXiv:2212.06817v2；[论文 HTML](https://arxiv.org/html/2212.06817v2)、[项目页](https://robotics-transformer1.github.io/) | Fig. 1–3；Table 2、7；§5–6 |
| [RT-2 PDF](./papers/RT-2_2307.15818v1.pdf) | Brohan et al., *RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control*，arXiv:2307.15818v1；[论文 HTML](https://arxiv.org/html/2307.15818v1)、[项目页](https://robotics-transformer2.github.io/) | Fig. 2–4；Table 7、8；§3–5 |

下载校验：RT-1 为 31 页，SHA-256 `81EFE669C8FA50FFC7097886DC78A442FA7A8F7F2451684B93069CB9FBEDA767`；RT-2 为 26 页，SHA-256 `0A62DC36BBBFDEA232AD45A0AB75C82E9CF535B55333FF22C02D5DA1897CCAC3`。本文只保存公开论文；没有附带模型权重或训练数据。

## 完成标准

1. 能写出 RT-1 的视觉 token 路径、语言注入方式、动作离散化和在线执行流程。
2. 能解释 RT-2 如何把预训练 VLM 接到机器人动作，并区别“预训练”“仅机器人微调”“网页与机器人数据联合训练”。
3. 能准确解释论文的 seen、unseen task、distractor、background、semantic/generalization 等评测各测了什么。
4. 能说清“懂得新物体/新指令”为什么不等于掌握新的运动技能，并指出推理速度与数据覆盖的约束。
5. 能把第 0 阶段的 ACT、Diffusion Policy 与 RT 系列放在同一控制问题下比较，避免跨硬件成功率直接排名。
