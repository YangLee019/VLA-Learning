# VLA-Learning

这是一个围绕 **视觉-语言-动作模型（Vision-Language-Action, VLA）与世界模型** 的学习型仓库。它保存原论文、用中文重建核心概念，并记录可检验的问题、实验想法和后续阅读路径。目标是形成自己的研究理解，而不只是收集论文标题。

## 如何使用

1. 按阶段阅读。从 [第 0 阶段：机器人模仿学习基础](./00-foundations/README.md) 开始，依次进入 [第 1 阶段：RT-1 与 RT-2](./01-rt-series/README.md)、[第 2 阶段：跨机器人数据与通用策略](./02-cross-embodiment/README.md)、[第 3 阶段：OpenVLA](./03-openvla/README.md)和[第 4 阶段：OpenVLA-OFT](./04-openvla-oft/README.md)。
2. 时间紧时以中文讲义为主线：先读导学与讲义，再按讲义标出的图表和章节核对本地论文 PDF，最后做带解析的复盘题。
3. 笔记中的流程图为本仓库绘制的概念示意；实验数字和具体实现以对应论文为准。
4. 在读论文时持续记录：**问题设定 → 输入与动作表示 → 模型与损失 → 数据 → 实验 → 局限**。

## 学习路线

| 阶段 | 主题 | 代表工作 |
| --- | --- | --- |
| 00 | 模仿学习、动作序列、连续动作生成 | ACT、Diffusion Policy |
| 01 | VLA 的形成 | RT-1、RT-2 |
| 02 | 多机器人数据与通用策略 | Open X-Embodiment、Octo |
| 03 | 开源 VLA 主线 | OpenVLA |
| 04 | 动作表示与推理效率 | OpenVLA-OFT |
| 05 | 连续动作 VLA | π₀、π₀.₅ |
| 06 | 经验学习与泛化 | π*₀.₆、π₀.₇ |
| 后续 | VLA 与世界模型的结合 | 视频预测、规划、想象式训练 |

目前已建立第 0–4 阶段；后续阶段在学习时逐步补充。仓库中的论文 PDF 是原始资料，中文笔记是可独立阅读的讲义，两者应一起使用。各阶段笔记篇数按主题复杂度安排。

## 仓库约定

- `NN-topic/papers/`：论文原文，文件名含论文名与 arXiv 编号或版本。
- `NN-topic/notes/`：可独立阅读的中文讲义，包含概念图、公式推导、训练与推理流程、实验边界和带解析的复盘题。
- 笔记优先链接本地 PDF，同时保留论文官方页面，方便核对版本。
- 外部网页用带说明文字的 Markdown 链接标在相关论述附近；每阶段 README 集中列出论文、项目和代码入口。
- 对尚未验证的推断明确标注为“我的理解”或“待验证”，避免与作者结论混淆。

## 第 0 阶段入口

- [阅读安排与论文清单](./00-foundations/README.md)
- [基础概念：从行为克隆到动作序列](./00-foundations/notes/00-基础概念.md)
- [ACT 精读笔记](./00-foundations/notes/01-ACT.md)
- [Diffusion Policy 精读笔记](./00-foundations/notes/02-Diffusion-Policy.md)
- [对照总结与自测](./00-foundations/notes/03-对照与自测.md)

## 第 1 阶段入口

- [阅读安排与论文清单](./01-rt-series/README.md)
- [从动作策略到语言条件](./01-rt-series/notes/00-从动作策略到语言条件.md)
- [RT-1 精读讲义](./01-rt-series/notes/01-RT-1.md)
- [RT-2 精读讲义](./01-rt-series/notes/02-RT-2.md)
- [对照、自测与研究问题](./01-rt-series/notes/03-对照与自测.md)

## 第 2 阶段入口

- [阅读安排、论文和官方资源](./02-cross-embodiment/README.md)
- [跨本体学习的基本问题](./02-cross-embodiment/notes/00-跨本体学习基础.md)
- [Open X-Embodiment 与 RT-X 精读讲义](./02-cross-embodiment/notes/01-Open-X-Embodiment.md)
- [Octo 精读讲义](./02-cross-embodiment/notes/02-Octo.md)
- [对照与带解析自测](./02-cross-embodiment/notes/03-对照与自测.md)

## 第 3 阶段入口

- [阅读安排、论文和官方资源](./03-openvla/README.md)
- [OpenVLA：模型、动作 token 与训练](./03-openvla/notes/01-模型与训练.md)
- [OpenVLA：实验、微调与局限](./03-openvla/notes/02-实验与微调.md)
- [OpenVLA：模型架构逐层拆解](./03-openvla/notes/03-模型架构逐层拆解.md)

## 第 4 阶段入口

- [阅读路线、论文与官方资源](./04-openvla-oft/README.md)
- [OpenVLA-OFT：架构与训练目标](./04-openvla-oft/notes/01-OFT架构与训练目标.md)
- [OpenVLA-OFT：消融实验、部署与研究判断](./04-openvla-oft/notes/02-消融实验与部署.md)
