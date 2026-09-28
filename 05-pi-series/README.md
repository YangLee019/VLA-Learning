# 第 5 阶段：π₀ 与 π₀.₅

本阶段把前四阶段的“视觉语言骨干 + 动作策略”接到两条新问题：**怎样对高频连续动作块建模**，以及**怎样让机器人在从未见过的家庭环境完成长时序任务**。π₀ 重点是 PaliGemma + flow matching 动作专家、跨机器人预训练与目标任务后训练；π₀.₅ 在此基础上，用 FAST 离散动作 token 预训练、语义子任务与网页数据共同训练，再加入连续动作专家，做统一模型的高低层推理。[π₀ 论文](https://arxiv.org/html/2410.24164v4)、[π₀.₅ 论文](https://arxiv.org/html/2504.16054v1)

## 快速学习路线

| 顺序 | 建议用时 | 材料 | 核心问题 |
| --- | ---: | --- | --- |
| 预备 | 15 分钟 | [OFT 架构与目标](../04-openvla-oft/notes/01-OFT架构与训练目标.md) | 连续 L1 动作块解决了什么，留下了什么？ |
| 1 | 75 分钟 | [π₀：模型架构与 flow matching](./notes/01-pi0-架构与训练.md) | 双专家如何共享注意力？噪声如何变成动作块？ |
| 2 | 75 分钟 | [π₀.₅：混合训练与高低层推理](./notes/02-pi05-架构与训练.md) | FAST、网页/子任务数据、后训练如何衔接？ |
| 3 | 50 分钟 | [FAST、实验对照与自测](./notes/03-FAST与研究对照.md) | 哪些结果证明动作表示、数据配方和语义分解的作用？ |

## 论文与官方资料

| 资源 | 阅读用途 |
| --- | --- |
| [π₀ 本地 PDF v4](./papers/pi0_2410.24164v4.pdf) · [HTML v4](https://arxiv.org/html/2410.24164v4) · [项目文章](https://physicalintelligence.company/blog/pi0) | 主论文：§III–VI、附录 A-B/A-D |
| [π₀.₅ 本地 PDF v1](./papers/pi0.5_2504.16054v1.pdf) · [HTML v1](https://arxiv.org/html/2504.16054v1) · [项目文章](https://pi.website/blog/pi05) | 主论文：§IV–V、附录 A-E |
| [FAST 本地 PDF v1](./papers/FAST_2501.09747v1.pdf) · [HTML v1](https://arxiv.org/html/2501.09747v1) · [项目页](https://pi.website/research/fast) | 补充：理解 π₀.₅ 为什么先用压缩后的离散动作序列预训练 |
| [openpi 官方实现](https://github.com/Physical-Intelligence/openpi) · [模型配置](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/models/pi0_config.py) | 检查模型接口、训练配置与开放检查点；代码持续变化，不能把当前 `main` 等同论文原始实验 |

本地 PDF 核验：π₀ v4 **17 页**，SHA-256 `FBDFBA56258BDBD220207BA63410C6C943E43A73E97A7A5A47CA0BC74204F821`；π₀.₅ v1 **19 页**，`6A1029FD8AB6944B74CF22F5E5D30E60BC15699D964B2900AF799B807A34B64C`；FAST v1 **19 页**，`3739B31F5FECDDE371509FF5BB13619979734E894A255A9B264253F4CC53934A`。仓库保存论文和讲义，不包含原始训练数据与模型权重。

## 本阶段的阅读边界

论文中的“预训练”有两层：PaliGemma 的互联网视觉语言预训练，以及之后的机器人数据预训练；后训练则是机器人任务适配。π₀.₅ 的网页数据在**机器人阶段共同训练**中再次出现，不能简单说“网页知识只来自 PaliGemma 初始化”。“open-world”指论文评测的**未见家庭环境与物体**，不是任意环境和任务的无条件保证。注意论文 PDF 的符号和细节偶有不一致，讲义会标明核对点。

## 学完应能回答

1. π₀ 的三个 attention block、双专家权重、50 个动作位置和 10 步积分各负责什么？
2. 为什么 π₀.₅ 先用 FAST 离散动作 token 训练，随后仍需要 flow matching 动作专家？
3. MM、ME、CE、HL、WD、VI 各提供哪类监督，消融能支持什么结论？
4. 一个 π₀.₅ 模型如何先输出文字子任务，再以该子任务为条件输出动作块？
5. “机器人 50 Hz 控制”“一次模型调用 73 ms”“每 25 步重规划”分别指什么？
