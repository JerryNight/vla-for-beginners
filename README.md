# VLA 入门手册

> 从零理解视觉-语言-动作模型（Vision-Language-Action）——一本读完能跟人正常讨论 VLA 的概念手册。

[![Docs](https://img.shields.io/badge/docs-online-success)](https://jerrynight.github.io/vla-for-beginners/)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/content-CC%20BY--NC--SA%204.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![License: MIT](https://img.shields.io/badge/code-MIT-blue)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](./CONTRIBUTING.md)

---

## 这本书想解决什么问题

搜 "VLA 是什么"，你会得到三种答案：

1. 一句正确的废话——「VLA 是把视觉、语言、动作统一到一个模型里」；
2. 一篇综述——罗列 80 个模型名和一堆缩写，读完还是不知道它怎么运作；
3. 一份工程教程——第一天就让你装 PyTorch、下 200GB 数据集、配 CUDA。

对没有服务器、没有机械臂、也还不确定自己要不要入这行的人来说，这三种都没用。

**这本书走第四条路：不写一行需要运行的代码，把概念从浅到深讲透。**

读完之后你应该能做到：

- 用大白话向别人解释 VLA 是什么、为什么会出现、卡在哪里；
- 看懂 RT-2、OpenVLA、π₀ 这些模型的架构图，知道每个模块在解决什么问题；
- 拿到一篇 VLA 新论文，能快速判断它属于哪条技术路线；
- 知道哪些宣传语是营销、哪些是真进展。

**明确不承诺的事**：读完你不会训出一个模型（这需要几十张 GPU 和一套机器人），也不会获得任何调参经验。这本书是地图，不是驾照。

## 门槛

| 需要 | 不需要 |
|---|---|
| 高中数学的直觉（知道「函数」「概率」大概是什么） | 微积分、线代证明 |
| 能读懂伪代码（看得懂 `for` 和 `if` 就够） | 会写 PyTorch |
| 一点好奇心 | GPU、机械臂、数据集 |

第 2.0 章专门为完全没接触过机器学习的人补了三个地基概念（向量、概率分布、损失函数），用类比讲，不推公式。**如果你连"神经网络"是什么都说不清，从那里开始完全没问题。**

## 全书主线

这本书不是章节的堆砌，所有内容都挂在同一条链上——**一句话如何变成一个动作**：

```
"把红杯子放到盘子上"
        │
        ▼  ① 语言编码 ──→ 一串向量
   ┌─────────┐
   │  对齐    │  ② 图和文在同一空间里相遇
   └─────────┘
        │
        ▼  ③ 融合 ──→ 一份"现在该干什么"的表征
   ┌─────────┐
   │ 动作解码 │  ④ 变成一个 7 维数字
   └─────────┘
        │
        ▼  ⑤ 执行、观察、再来一次（闭环）
   机械臂动了
```

每一章都在回答这条链上的一个具体问题。读的时候如果迷路了，回到这张图。

## 目录

**第一部分 · 先把误解拆掉**
- [1.1 关于 VLA 的五个误解](docs/part0-why/00-five-misconceptions.md)
- [1.2 为什么非要 VLA](docs/part0-why/01-why-vla.md)
- [1.3 VLA 的一句话定义](docs/part0-why/02-definition.md)

**第二部分 · 三个词拆开看**
- [2.0 读后面所有章节前，先补三个地基](docs/part1-three-words/03-prerequisites.md)
- [2.1 视觉：一张图怎么变成一串数字](docs/part1-three-words/04-vision.md)
- [2.2 语言：机器怎么"听懂"人话](docs/part1-three-words/05-language.md)
- [2.3 动作：机器人怎么"动"才算动](docs/part1-three-words/06-action.md)

**第三部分 · 怎么把三者连起来**
- [3.1 对齐：CLIP 为什么是分水岭](docs/part2-connecting/07-alignment.md)
- [3.2 融合：三股信息在哪里合流](docs/part2-connecting/08-fusion.md)
- [3.3 动作解码：三种把想法变成数字的流派](docs/part2-connecting/09-action-head.md)

**第四部分 · 训练到底在训练什么**
- [4.1 数据：一条机器人训练数据长什么样](docs/part3-training/10-data.md)
- [4.2 行为克隆：模仿学习为什么会翻车](docs/part3-training/11-behavior-cloning.md)
- [4.3 预训练与后训练：常识从哪来，动作从哪来](docs/part3-training/12-pretrain.md)

**第五部分 · 模型谱系地图**
- [5.1 谱系总览：五年，五个转折](docs/part4-map/13-lineage.md)
- [5.2 π₀ 与流匹配：为什么它把速度提到了 50Hz](docs/part4-map/14-pi0.md)
- [5.3 分层 VLA：让大脑和小脑分工](docs/part4-map/15-hierarchical.md)

**第六部分 · 诚实的部分**
- [6.1 两个卡脖子的硬约束](docs/part5-reality/16-bottlenecks.md)
- [6.2 泛化与评测：怎么判断一个 VLA 是真行还是演得好](docs/part5-reality/17-evaluation.md)

**第七部分 · 接下来怎么走**
- [7.1 三条不同的继续学习路径](docs/part6-next/18-how-to-continue.md)

**附录**
- [术语表（中英对照）](docs/appendix/glossary.md)
- [论文与资源清单](docs/appendix/papers.md)
- [零硬件游乐场](docs/appendix/playground.md)
- [常见问题](docs/appendix/faq.md)

## 本地起一个站点

```bash
pip install mkdocs-material
mkdocs serve          # 打开 http://127.0.0.1:8000
```

纯 Markdown 也能读，`docs/` 下的文件在 GitHub 网页上可以直接打开，只是没有搜索和侧边栏。

## 参与贡献

发现讲错了、类比不贴切、或者某个概念你觉得有更好的解释方式，欢迎提 Issue 或 PR。

尤其欢迎这两类反馈：
- **「我卡在这里没看懂」**——这是最有价值的反馈，说明类比失败了；
- **指出与最新论文不符的地方**——这个领域半年就换一轮，书里肯定有跟不上的部分。

细节见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 许可

- 文字内容：[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)——可自由转载、改编，需署名、非商用、相同方式共享
- 代码与配置：MIT

---

<p align="center"><sub>如果这本书帮你省下了三天乱翻论文的时间，给它点个 star 就是最好的回报。</sub></p>
