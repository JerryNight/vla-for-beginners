# 论文与资源清单

## 如果只读五篇

按这个顺序，不要跳。

| # | 论文 | 年份 | 为什么是它 |
|---|---|---|---|
| 1 | **ACT**: Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware | 2023 | 动作块（action chunk）的源头。读完你就懂为什么 VLA 要一次输出一段动作 |
| 2 | **RT-2**: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control | 2023 | VLA 这个概念的起点。把动作当 token 的第一次严肃尝试 |
| 3 | **OpenVLA**: An Open-Source Vision-Language-Action Model | 2024 | 开源可复现，代码能跑，是理解工程细节最好的入口 |
| 4 | **π₀**: A Vision-Language-Action Flow Model for General Robot Control | 2024 | 流匹配 + 50 Hz，当前主流范式 |
| 5 | **π₀.₅**: a Vision-Language-Action Model with Open-World Generalization | 2025 | 分层 + 开放世界泛化，代表最新方向 |

**为什么这个顺序**：先懂「动作怎么生成」（ACT），再懂「语言怎么进来」（RT-2），再懂「工程怎么做」（OpenVLA），最后懂「怎么做到又好又快」（π₀ 系列）。

---

## 前史：VLA 之前的关键工作

不了解这些，就看不懂 VLA 在继承什么。

| 论文 | 年份 | 一句话 |
|---|---|---|
| **CLIP**: Learning Transferable Visual Models From Natural Language Supervision | 2021 | 图文对齐的地基。没有它，VLA 不存在 |
| **SayCan**: Do As I Can, Not As I Say | 2022 | LLM 做高层规划，底层调用技能库。分层的源头 |
| **Gato**: A Generalist Agent | 2022 | 一个 Transformer 干所有事。过于激进，但方向对 |
| **PaLM-E**: An Embodied Multimodal Language Model | 2023 | 把图像编码进语言模型，VLM 进机器人的第一步 |
| **Diffusion Policy**: Visuomotor Policy Learning via Action Diffusion | 2023 | 机器人怎么用扩散。必读，虽然不是 VLA |
| **Octo**: An Open-Source Generalist Robot Policy | 2024 | 开源通用策略，比 OpenVLA 轻，适合资源有限时参考 |

---

## 数据集与开源项目

| 名称 | 是什么 | 适合谁 |
|---|---|---|
| **Open X-Embodiment (OXE)** | 22 种机器人、100 万+ 轨迹的统一数据集 | 想做跨本体研究的人 |
| **DROID** | 7.6 万条真实场景数据，13 个机构 | 想要场景多样性的 |
| **BridgeData** | 早期重要数据集，厨房场景 | 做对比实验的 |
| **LeRobot**（HuggingFace） | 数据集 + 模型 + 训练框架，格式最友好 | **新手首选** |
| **OpenVLA** | 7B 开源 VLA，含权重和训练代码 | 想微调自己模型的 |
| **LIBERO** | 130 个任务的仿真基准 | 做 benchmark 对比的 |
| **CALVIN** | 长程语言条件操作基准 | 测连续指令跟随的 |
| **SimplerEnv** | 与真机对齐的仿真环境 | 想让仿真结果可信的 |

**入门建议**：从 LeRobot 开始，它有完整的「下载数据 → 训练 → 推理」流程，而且不需要真机。

---

## 综述

如果你想要一张更全的地图，读综述。但注意：综述写得快、更新慢，2026 年的综述里可能缺 2026 年的进展。

| 综述 | 特点 |
|---|---|
| **Vision-Language-Action Models for Robotics: A Review Towards Real-World Applications**（IEEE Access 2025） | 覆盖面广，带一个可筛选的模型数据库网站 |
| **A Survey on Vision-Language-Action Models: An Action Tokenization Perspective** | 专门讲动作怎么离散化，角度独特 |
| **Vision-Language-Action Models for Embodied AI**（2026） | 最新的综合梳理，按架构/数据/评测/应用四支柱组织 |

---

## 怎么读一篇 VLA 论文

按这个顺序，20 分钟能判断一篇论文值不值得细读。

### 第一步：看架构图（2 分钟）

只看图，问三个问题：

1. **主干是什么？** VLM 微调，还是从零训练？
2. **动作头是什么？** 自回归 / 扩散 / 流匹配？
3. **融合在哪一层？** 早期（拼序列）/ 晚期（拼特征）/ 交叉注意力？

三个问题答完，你已经知道它的性格了。

### 第二步：看数据（3 分钟）

- 用了多少条轨迹？
- 自采的还是公开的？
- 几种机器人？

**数据规模直接决定了它能力的上限。** 一篇用 5000 条数据训出来的模型宣称「强泛化」，基本可以打折。

### 第三步：看评测（5 分钟）

- 仿真还是真机？
- 有没有泛化矩阵（新物体/新场景/新指令/新本体）？
- 有没有报失败模式？
- 有没有和强 baseline 比？

**这一节最能暴露水分**，详见[第 6.2 节](../part5-reality/17-evaluation.md)的危险信号清单。

### 第四步：看方法细节（10 分钟）

只挑你关心的部分看：

- 关心速度 → 看去噪步数、动作块长度、参数量
- 关心精度 → 看动作表示（欧拉角还是 6D）、归一化方式
- 关心泛化 → 看数据配比、有没有做指令增强

### 第五步：决定要不要复现

看有没有开源权重、代码质量、issue 区是否活跃。

**issue 区是最真实的信息源**——论文不会告诉你「这个模型在什么情况下会崩」，但 issue 区会。

---

## 追踪进展的三个渠道

1. **CoRL / ICRA / RSS 的录用列表** —— 每年两次，看清当年什么值得看
2. **20 个左右的活跃研究者**（X/Twitter）—— 他们的转发比论文列表有信息量
3. **开源项目的 issue 区** —— 真实的坑都在这里

**不要刷 arXiv 全站。** 每天几十篇，九成是噪声。
