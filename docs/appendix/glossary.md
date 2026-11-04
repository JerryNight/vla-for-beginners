# 术语表（中英对照）

这个领域的术语混乱程度堪称灾难。同一个东西有三四个名字，同一个名字有时指两件事。

按类别整理，每个词给一句人话解释。

---

## 一、模型与架构

| 中文 | 英文 | 一句话解释 |
|---|---|---|
| 视觉-语言-动作模型 | VLA (Vision-Language-Action) | 输入图和话、输出动作的模型 |
| 视觉-语言模型 | VLM | 只看图和话、输出文本的模型，VLA 的前身 |
| 大语言模型 | LLM | 只看文本、输出文本 |
| 主干 / 底座 | backbone | 模型的主体网络，通常是一个预训练的 VLM |
| 动作头 | action head / action expert | 把特征变成动作数字的那一小块网络 |
| 编码器 | encoder | 把输入变成向量的模块 |
| 解码器 | decoder | 把向量变成输出的模块 |
| 投影层 | projector / projection layer | 把维度对齐的那个线性层，架构图里的小方块 |
| 交叉注意力 | cross-attention | 一方去「检索」另一方信息的机制 |
| 前缀 / 词元 | token | 模型处理的最小单位，图像块和词都是一个 token |
| 位置编码 | positional encoding | 告诉模型「这个 token 原来在哪」 |
| 分层 VLA | hierarchical VLA | 高层规划 + 低层执行的两级结构 |
| 双系统 | dual-system | System 1（快反射）+ System 2（慢思考） |

---

## 二、训练与数据

| 中文 | 英文 | 一句话解释 |
|---|---|---|
| 轨迹 / 回合 | trajectory / episode | 一次完整的操作记录，从开始到结束 |
| 示教 | demonstration | 人做一遍给机器看的数据 |
| 遥操作 | teleoperation | 人远程操控机器人来采集数据 |
| 行为克隆 | behavior cloning (BC) | 模仿学习：学着复现专家的动作 |
| 模仿学习 | imitation learning | 从示教中学习，行为克隆是其中一种 |
| 分布漂移 | distribution shift | 部署时遇到训练没见过的状态 |
| 复合误差 | compounding error | 小误差累积成大偏差 |
| 预训练 | pretraining | 在大规模通用数据上先训一轮 |
| 后训练 / 微调 | post-training / fine-tuning | 在目标任务的小数据上再训 |
| 灾难性遗忘 | catastrophic forgetting | 微调之后把原来会的东西忘了 |
| 对比学习 | contrastive learning | 拉近正样本、推远负样本的训练方式 |
| 零样本 | zero-shot | 没在训练里见过，直接就能做 |
| 少样本 | few-shot | 给几个例子就能做 |
| 数据配比 | data mixture | 混多个数据集时的采样权重 |
| 动作块 | action chunk | 一次预测未来多步动作 |
| 预测视野 | horizon (H) | 一次预测覆盖多少步 |

---

## 三、机器人基础

| 中文 | 英文 | 一句话解释 |
|---|---|---|
| 本体 / 具身 | embodiment | 具体那台机器人的身体 |
| 末端执行器 | end-effector | 机械臂末端的东西，通常是夹爪 |
| 夹爪 | gripper | 抓东西的装置 |
| 自由度 | DoF (degree of freedom) | 能独立运动的维度数 |
| 关节空间 | joint space | 用每个关节的角度来描述状态 |
| 笛卡尔空间 | Cartesian space | 用末端在xyz坐标里的位置来描述状态 |
| 正运动学 | forward kinematics (FK) | 已知关节角，算出末端在哪 |
| 逆运动学 | inverse kinematics (IK) | 已知末端要去哪，算出关节该转多少 |
| 本体感知 | proprioception | 机器人对自己状态的感知（关节角、力矩） |
| 工作空间 | workspace | 机械臂能到达的空间范围 |
| 跨本体 | cross-embodiment | 一个模型适配多种不同的机器人 |
| 仿真到现实 | sim-to-real | 在仿真里训练，搬到真机上用 |

---

## 四、动作与动作生成

| 中文 | 英文 | 一句话解释 |
|---|---|---|
| 动作向量 | action vector | 一组描述动作的数字，通常 7 或 10 维 |
| 增量动作 | delta action | 相对于当前状态的位移，不是绝对坐标 |
| 欧拉角 | Euler angles | 用三个角度表示旋转，有万向锁问题 |
| 四元数 | quaternion | 用四个数表示旋转，有双重覆盖问题 |
| 六维旋转表示 | 6D rotation representation | 用旋转矩阵前两列表示，当前主流 |
| 万向锁 | gimbal lock | 欧拉角在特定角度失去一个自由度 |
| 自回归 | autoregressive | 一个 token 一个 token 地生成 |
| 扩散 | diffusion | 从噪声出发，迭代去噪生成结果 |
| 流匹配 | flow matching | 学一个速度场，沿直线从噪声走到结果 |
| 去噪步数 | denoising steps | 生成过程中迭代多少次 |
| 模式平均 | mode averaging | 多峰分布被平均成一个不存在的中间值 |
| 多峰分布 | multimodal distribution | 同一情况有多个合理答案的分布 |
| 归一化 | normalization | 把动作缩放到统一范围，通常 [-1, 1] |

---

## 五、评测与泛化

| 中文 | 英文 | 一句话解释 |
|---|---|---|
| 成功率 | success rate | 跑 N 次成功几次 |
| 泛化 | generalization | 在训练分布之外表现好 |
| 开放词汇 | open-vocabulary | 能识别训练里没出现过的类别 |
| 长程任务 | long-horizon task | 需要很多步才能完成的任务 |
| 干扰测试 | perturbation test | 故意改变条件看它还能不能做 |
| 基准 | benchmark | 标准化的一批测试任务 |

---

## 六、几个容易混的概念

**VLA vs VLM vs LLM**

```text
LLM：文字 → 文字
VLM：图 + 文字 → 文字
VLA：图 + 文字 → 动作（可能附带文字）
```

**具身智能 vs VLA**

具身智能（Embodied AI）是一个大领域，指「有身体的智能」。VLA 是目前这个领域最主流的一条技术路线，但不是唯一的路（还有纯强化学习、纯规划等）。

**策略 vs 模型**

「策略（policy）」强调的是「输入状态输出动作」这个函数关系，「模型」强调的是网络结构。日常混用，但严格说 π 是策略，Transformer 是模型。

**动作块 vs 动作序列**

动作块（action chunk）特指「一次推理生成的一段」，强调「一次性生成」。动作序列可以指任何一段动作。

**预训练 vs 后训练 vs 微调**

预训练 = 大规模通用数据上先训；后训练 = 在目标任务上再训；微调 = 后训练的一种具体形式。日常混用。

---

## 七、缩写速查

| 缩写 | 全称 | 中文 |
|---|---|---|
| VLA | Vision-Language-Action | 视觉-语言-动作 |
| VLM | Vision-Language Model | 视觉语言模型 |
| LLM | Large Language Model | 大语言模型 |
| BC | Behavior Cloning | 行为克隆 |
| ACT | Action Chunking with Transformers | 带动作块的 Transformer 策略 |
| OXE | Open X-Embodiment | 开放跨本体数据集 |
| DoF | Degree of Freedom | 自由度 |
| IK / FK | Inverse / Forward Kinematics | 逆 / 正运动学 |
| CoRL | Conference on Robot Learning | 机器人学习会议 |
| ICRA | Int. Conf. on Robotics and Automation | 国际机器人与自动化会议 |
| RSS | Robotics: Science and Systems | 机器人科学与系统会议 |
