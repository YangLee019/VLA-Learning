# 第 0 阶段：模仿学习与连续动作生成

**目标：**在进入 RT-1、OpenVLA 和 π 系列之前，先能解释机器人策略如何从示范中学习，以及为何常常一次预测一段动作。

## 学习顺序

| 顺序 | 材料 | 重点 | 建议产出 |
| --- | --- | --- | --- |
| 1 | [基础概念](./notes/00-基础概念.md) | 观察、状态、动作、行为克隆、分布偏移 | 画出一次闭环控制流程 |
| 2 | [ACT 原论文](./papers/ACT_2304.13705.pdf) → [笔记](./notes/01-ACT.md) | action chunk、时间集成、CVAE | 用一句话解释每个模块的作用 |
| 3 | [Diffusion Policy 原论文](./papers/Diffusion_Policy_2303.04137v5.pdf) → [笔记](./notes/02-Diffusion-Policy.md) | 条件扩散、去噪损失、滚动时域执行 | 解释三个时间窗口的区别 |
| 4 | [对照与自测](./notes/03-对照与自测.md) | 两种动作生成方法的共同点与差异 | 不看答案独立回答问题 |

建议先看论文的摘要、问题设定、方法图与结论，再阅读具体公式、实验和局限。两篇论文的硬件、任务和评价设置不同，**不要直接拿它们报告的成功率做模型优劣排名**。

## 原论文与版本

| 文件 | 论文 | 来源 | 本地校验 |
| --- | --- | --- | --- |
| [ACT_2304.13705.pdf](./papers/ACT_2304.13705.pdf) | Zhao et al., *Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware*, 2023，arXiv v1 | [arXiv](https://arxiv.org/abs/2304.13705)、[项目页](https://tonyzhaozh.github.io/aloha/) | 18 页；SHA-256 `2E2FE25860F5F9CEE9E655A2714E9F2264A7A5078BCD267C16D3F39AF461345A` |
| [Diffusion_Policy_2303.04137v5.pdf](./papers/Diffusion_Policy_2303.04137v5.pdf) | Chi et al., *Diffusion Policy: Visuomotor Policy Learning via Action Diffusion*, arXiv v5（IJRR 2024 扩展版） | [arXiv](https://arxiv.org/abs/2303.04137)、[项目页](https://diffusion-policy.cs.columbia.edu/) | 19 页；SHA-256 `B65C474B696A4802D8F1457D86B637CE2C5521412570D3AA928CD54563BABC8F` |

## 完成标准

- 能区分机器人真实状态、传感器观察、自身关节状态和控制动作。
- 能说明单步行为克隆的误差为何会在闭环执行中累积。
- 能解释 action chunk 如何改变决策频率，以及为什么过长的 chunk 会降低反应性。
- 能写出 ACT 与 Diffusion Policy 各自如何生成一段动作。
- 能说出两篇工作的至少一个局限，并指出下一阶段 VLA 为何还要引入语言和大规模预训练。
