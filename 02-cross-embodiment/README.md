# 第 2 阶段：跨机器人数据与通用策略

第 1 阶段的 RT-1、RT-2 主要在特定机器人数据上研究语言条件控制与网页知识迁移。本阶段问：**能否把不同机器人的示范汇集起来，让一个策略吸收其他平台的经验，并能以少量新机器人数据适配？**主线是 Open X-Embodiment（OXE）及 RT-X，然后是 Octo。

## 先读讲义，再按需核查论文

| 顺序 | 建议用时 | 材料 | 阅读目标 |
| --- | ---: | --- | --- |
| 1 | 15 分钟 | [跨本体学习的基本问题](./notes/00-跨本体学习基础.md) | 区分统一存储、动作对齐与真正的跨本体泛化 |
| 2 | 35 分钟 | [Open X-Embodiment 与 RT-X 讲义](./notes/01-Open-X-Embodiment.md) | 理解数据来源、RLDS、动作转换、正/负迁移和实验范围 |
| 3 | 40 分钟 | [Octo 讲义](./notes/02-Octo.md) | 理解可扩展 token 接口、扩散动作头、预训练与新本体微调 |
| 4 | 20 分钟 | [对照与带解析自测](./notes/03-对照与自测.md) | 解释 zero-shot 与少样本微调各证明了什么 |

讲义可独立阅读；图是本仓库重绘的示意。核对时优先看下面指出的图、表和小节。**网页链接用带说明文字的 Markdown 链接放在论述附近**，集中入口也列在这里；本地 PDF 是固定版本，网页内容可能更新。

## 原论文与官方资源

| 资料 | 用途 | 优先核对 |
| --- | --- | --- |
| [OXE / RT-X 本地 PDF](./papers/Open_X_Embodiment_2310.08864v9.pdf) · [arXiv 论文与版本](https://arxiv.org/abs/2310.08864) · [项目页](https://robotics-transformer-x.github.io/) | 22 种本体的数据资源、RT-1-X / RT-2-X 实验 | Fig. 1–4、Table I–II、§III–VI |
| [Octo 本地 PDF](./papers/Octo_2405.12213v2.pdf) · [arXiv 论文与版本](https://arxiv.org/abs/2405.12213) · [项目页](https://octo-models.github.io/) | 基于 OXE 的开放通用策略 | Fig. 1–5、Table I–II、§III–V |
| [OXE 官方代码与数据入口](https://github.com/google-deepmind/open_x_embodiment) | 查看数据集清单、读取接口和获取方式 | 与论文版本、使用条款分别核对 |
| [Octo 官方代码](https://github.com/octo-models/octo) | 查看模型、检查点、数据加载和微调范例 | 代码可能晚于论文更新 |

本地文件校验：OXE PDF **12 页**，SHA-256 `13F16AFF5AFDEE583DC25B3C570E9BB0CF6BAEFB59B539928D919588CD8D9246`；Octo PDF **17 页**，SHA-256 `73BFF297CFAFE523319162124E6B7F96919C0930E0A380F307255C4C7464AC93`。本阶段只保存论文 PDF，不在仓库复制 TB 级机器人数据或模型权重。

## 必须记住的三个数据范围

| 名称 | 论文中的范围 | 不应误写为 |
| --- | --- | --- |
| OXE 完整资源 | 60 个来源数据集、22 种机器人本体、逾 100 万条轨迹 | 所有 RT-X 实验都用全部数据 |
| RT-X 论文的机器人训练混合 | 实验时可用的约 9 种本体；论文的 RT-X 子集约 35 万条轨迹（Octo 论文回顾口径） | 与完整 OXE 等量 |
| Octo 训练混合 | 从 OXE 筛选 25 个数据集、约 80 万条轨迹 | “直接不加筛选训练全部 OXE” |

来源：[OXE 论文 §III–IV](https://arxiv.org/html/2310.08864v9#S3)、[Octo 论文 §III-B](https://arxiv.org/html/2405.12213v2#S3.SS2)。不同论文版本/统计口径下总量会变动，比较时应同时报告数据版本、筛选规则和样本单位。

## 完成标准

- 能解释 RLDS 统一**数据组织**，为何不自动统一机器人坐标系和动作语义。
- 能画出 OXE → RT-1-X / RT-2-X 与 OXE 子集 → Octo 的两条训练路径，并标出各自数据范围。
- 能用论文的正迁移和负迁移结果分析模型容量、数据多样性与目标域数据量的关系。
- 能解释 Octo 的语言/目标图像输入、block-wise attention、readout token、连续扩散动作块和微调接口。
- 能区分“在预训练机器人和任务上的 zero-shot 执行”“对新设置少样本微调”和“完全未见机器人零样本控制”。
