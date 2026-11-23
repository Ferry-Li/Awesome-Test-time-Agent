# Awesome 智能体测试时改进

![语言模型智能体如何在测试时改进](assets/banner.zh-CN.svg)

[![Awesome](assets/awesome.svg)](https://awesome.re/) [![English](assets/english.svg)](README.md) [![简体中文](assets/chinese.svg)](README.zh-CN.md)

> [!NOTE]
> **综述论文** · [PDF](main.pdf)
>
> *Test-Time Improvement in LLM Agents: A Survey of Mechanisms, Protocols, and Evaluation*

---

<a name="overview"></a>

### ✨ 概览

一次测试失败后，智能体可以修订当前答案、为后续任务留下经验，也可以再做一次检查。这份清单沿着这三条线索，梳理智能体如何将执行时获得的证据用于决策。

以下按主题列出 **190 篇文献**，包括[文献登记表](evidence_matrix.csv)中的 189 篇，以及引言另引的一篇自主智能体综述。[综述总览图](assets/survey-overview.png)展示各主题之间的联系。

> [!IMPORTANT]
> **推荐论文或更正条目**
>
> 欢迎通过 Issue 或 Pull Request 提交原论文链接、所属主题，以及一句机制说明。若补充代码，请附作者仓库。

---

### 📚 目录

- [🧭 决策时改进](#decisions)
  - [评价与选择 (14)](#selection)
  - [反馈引导的修订 (9)](#revision)
  - [搜索与探索 (20)](#search)
  - [基于模型的前瞻 (7)](#lookahead)
- [🧠 基于经验的适应](#adaptation)
  - [构建记忆 (8)](#memory)
  - [检索并使用经验 (9)](#retrieval)
  - [技能与程序 (5)](#skills)
  - [模型更新与更新规则 (20)](#updates)
- [🎛️ 自适应改进控制](#control)
  - [安排推理与交互 (3)](#timing)
  - [分配额外计算 (8)](#allocation)
  - [路由与协作 (7)](#routing)
  - [重试与停止 (1)](#stopping)
- [📏 评估协议](#evaluation)
  - [搜索、计算与交互预算 (6)](#evaluation-search)
  - [验证与反馈可靠性 (8)](#evaluation-verification)
  - [记忆、迁移与连续任务 (9)](#evaluation-memory)
- [📖 训练与理论背景](#background)
  - [智能体训练与系统设计 (13)](#training)
  - [训练信号与奖励设计 (13)](#rewards)
  - [理论基础与对照方法 (18)](#foundations)
- [📚 相关综述](#surveys)
  - [综述论文 (12)](#survey-papers)

---

<a name="decisions"></a>

### 🧭 决策时改进

智能体可以怎样利用当前可获得的证据来改进行动？第 3 章比较四种作用于当前决策的操作。

<a name="selection"></a>

#### 评价与选择 (14)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Agentic Reward Modeling: Verifying GUI Agent via Progressive Trajectory-Grounded Interaction](https://arxiv.org/html/2602.00575v2)** | arXiv | 2026 | 结合轨迹和界面探查结果核验智能体行为。 | — |
| **[Agentic Rubrics as Contextual Verifiers for SWE Agents](https://aclanthology.org/2026.acl-long.697/)** | ACL | 2026 | 根据仓库信息建立评价准则，检查候选补丁。 | — |
| **[AgentV-RL: Scaling Reward Modeling with Agentic Verifier](https://aclanthology.org/2026.findings-acl.1156/)** | Findings of ACL | 2026 | 让验证器主动获取奖励判断所需的证据。 | — |
| **[KV-PRM: Efficient Process Reward Modeling via KV-Cache Transfer for Multi-Agent Test-Time Scaling](https://arxiv.org/abs/2607.09153)** | arXiv | 2026 | 通过迁移 KV 缓存降低过程奖励评分开销。 | — |
| **[LLM-as-a-Verifier: A General-Purpose Verification Framework](https://arxiv.org/html/2607.05391v2)** | arXiv | 2026 | 拆分评估准则并汇总多次判断。 | — |
| **[ToolPRM: Fine-Grained Inference Scaling of Structured Outputs for Function Calling](https://aclanthology.org/2026.acl-long.855/)** | ACL | 2026 | 评估候选工具调用的结构与参数。 | — |
| **[AgentPRM: Process Reward Models for LLM Agents via Step-Wise Promise and Progress](https://arxiv.org/abs/2511.08325)** | arXiv | 2025 | 同时评价预期成功率和中间一步带来的相对进展。 | — |
| **[AgentRM: Enhancing Agent Generalization with Reward Modeling](https://arxiv.org/abs/2502.18407)** | ACL | 2025 | 用奖励或模型判断选择候选解并引导扩展。 | — |
| **[MASPRM: Multi-Agent System Process Reward Model](https://arxiv.org/abs/2510.24803)** | arXiv | 2025 | 研究如何用过程奖励评估多智能体系统的中间步骤。 | — |
| **[Process Reward Models for LLM Agents: Practical Framework and Directions](https://arxiv.org/abs/2502.10325)** | arXiv | 2025 | 用采样得到的后续回报估计动作价值，给候选动作排序。 | — |
| **[RoboMonkey: Scaling Test-Time Sampling and Verification for Vision-Language-Action Models](https://proceedings.mlr.press/v305/kwok25a.html)** | CoRL | 2025 | 为视觉语言动作策略结合采样与验证。 | — |
| **[RoVer: Robot Reward Model as Test-Time Verifier for Vision-Language-Action Model](https://arxiv.org/abs/2510.10975)** | arXiv | 2025 | 在测试时用机器人奖励模型验证候选动作。 | — |
| **[Web-Shepherd: Advancing PRMs for Reinforcing Web Agents](https://arxiv.org/abs/2505.15277)** | NeurIPS | 2025 | 根据任务要求检查网页操作轨迹。 | — |
| **[Enhancing Decision-Making for LLM Agents via Step-Level Q-Value Models](https://arxiv.org/abs/2409.09345)** | arXiv | 2024 | 逐步估计智能体轨迹中的动作价值。 | — |

<a name="revision"></a>

#### 反馈引导的修订 (9)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[CURE: Critique-Driven Unified Reinforcement Learning for Test-Time Self-Improvement](https://aclanthology.org/2026.acl-long.1321/)** | ACL | 2026 | 用批评反馈改进推理，并比较 token 消耗与延迟。 | — |
| **[Inference-Time Scaling of Verification: Self-Evolving Deep Research Agents via Test-Time Rubric-Guided Verification](https://aclanthology.org/2026.findings-acl.1243/)** | Findings of ACL | 2026 | 依据分项评价指出的问题修订研究型回答。 | — |
| **[GenPilot: A Multi-Agent System for Test-Time Prompt Optimization in Image Generation](https://arxiv.org/html/2510.07217v1)** | arXiv | 2025 | 依据此前生成结果中的错误修改图像提示词。 | — |
| **[Mapping Smarter, Not Harder: A Test-Time Reinforcement Learning Agent That Improves Without Labels or Model Updates](https://aclanthology.org/2025.emnlp-industry.75/)** | EMNLP Industry | 2025 | 针对含义不清的字段补充检索，再修订映射。 | — |
| **[Planning without Search: Refining Frontier LLMs with Offline Goal-Conditioned RL](https://proceedings.neurips.cc/paper_files/paper/2025/hash/0e87f947391341256517bdc5d206e539-Abstract-Conference.html)** | NeurIPS | 2025 | 根据学习到的价值估计形成文字反馈，指导修订。 | — |
| **[S2R: Teaching LLMs to Self-verify and Self-correct via Reinforcement Learning](https://aclanthology.org/2025.acl-long.1104/)** | ACL | 2025 | 通过强化学习训练模型检查并修正自己的答案。 | — |
| **[Two Heads Are Better Than One: Dual-Model Verbal Reflection at Inference-Time](https://aclanthology.org/2025.emnlp-main.155/)** | EMNLP | 2025 | 在推理阶段用两个模型进行语言反思。 | — |
| **[When Agents go Astray: Course-Correcting SWE Agents with PRMs](https://arxiv.org/abs/2509.02360)** | arXiv | 2025 | 识别软件修复轨迹中的无效步骤以调整探索方向。 | — |
| **[Reflexion: Language Agents with Verbal Reinforcement Learning](https://proceedings.neurips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html)** | NeurIPS | 2023 | 将失败经验写成反思，用于指导下一次尝试。 | [GitHub](https://github.com/noahshinn/reflexion) [![Stars](https://img.shields.io/github/stars/noahshinn/reflexion?style=social&label=Stars)](https://github.com/noahshinn/reflexion/stargazers) |

<a name="search"></a>

#### 搜索与探索 (20)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[A Reward-Guided Dual-Phase Framework for Adaptive Inference-Time Reasoning](https://aclanthology.org/2026.findings-acl.511/)** | Findings of ACL | 2026 | 用奖励引导分为两个阶段的推理过程。 | — |
| **[Agentic Monte Carlo: Simulating Reinforcement Learning for Black-Box Agents](https://arxiv.org/abs/2606.05296)** | arXiv | 2026 | 研究仅能通过黑盒接口调用的智能体如何分配采样。 | — |
| **[Continuous Improvement and Parallel Autonomous Exploration: An LLM-Agent Framework for Searching Large Solution Spaces](https://arxiv.org/html/2608.04341v1)** | arXiv | 2026 | 用多个智能体并行探索较大的解空间。 | — |
| **[FlowPIE: Test-Time Scientific Idea Evolution with Flow-Guided Literature Exploration](https://arxiv.org/html/2603.29557v1)** | arXiv | 2026 | 通过文献探索在测试时修订候选科研想法。 | — |
| **[LLM Inductive Reasoning Through Multi-Agent Enhanced Monte Carlo Tree Search](https://aclanthology.org/2026.findings-acl.1178/)** | Findings of ACL | 2026 | 在面向归纳推理的多智能体树搜索中检验候选假设。 | — |
| **[SWE-TRACE: Optimizing Long-Horizon SWE Agents Through Rubric Process Reward Models and Heuristic Test-Time Scaling](https://arxiv.org/abs/2604.14820)** | arXiv | 2026 | 用基于准则的过程奖励指导长程软件任务中的搜索。 | — |
| **[Table-as-Search: Agentic Information Seeking is Table Completion](https://aclanthology.org/2026.findings-acl.743/)** | Findings of ACL | 2026 | 将智能体的信息搜索表述为表格补全。 | — |
| **[Test-Time Strategies for More Efficient and Accurate Agentic RAG](https://arxiv.org/html/2603.12396v1)** | arXiv | 2026 | 比较检索增强智能体在测试阶段的求解策略。 | — |
| **[Thinking with Map: Reinforced Parallel Map-Augmented Agent for Geolocalization](https://aclanthology.org/2026.findings-acl.894/)** | Findings of ACL | 2026 | 结合地图信息与并行推理完成地理定位。 | — |
| **[Uncertainty-Aware Test-Time Search for Optimization Problem Solving](https://aclanthology.org/2026.acl-long.1975/)** | ACL | 2026 | 借助求解器反馈检查优化问题建模的可行性。 | — |
| **[VOLTS: Validated Output through Logit Tree Search for Reliable PDDL Planning with Small Language Models](https://proceedings.mlr.press/v318/massad26a.html)** | Canadian AI | 2026 | 依据 PDDL 前置条件和动作效果验证规划步骤。 | — |
| **[MASTER: A Multi-Agent System with LLM Specialized MCTS](https://aclanthology.org/2025.naacl-long.476/)** | NAACL | 2025 | 在多智能体系统中使用专门设计的蒙特卡洛树搜索。 | — |
| **[QLASS: Boosting Language Agent Inference via Q-Guided Stepwise Search](https://proceedings.mlr.press/v267/lin25l.html)** | ICML | 2025 | 使用逐步 Q 值估计引导推理路径扩展。 | — |
| **[Step-level Verifier-guided Hybrid Test-Time Scaling for Large Language Models](https://aclanthology.org/2025.emnlp-main.931/)** | EMNLP | 2025 | 结合逐步验证、局部修订与并行搜索。 | — |
| **[Thinking Longer, Not Larger: Enhancing Software Engineering Agents via Scaling Test-Time Compute](https://arxiv.org/html/2503.23803v2)** | arXiv | 2025 | 研究额外测试时计算对软件工程智能体的影响。 | — |
| **[Agent Q: Advanced Reasoning and Learning for Autonomous AI Agents](https://arxiv.org/abs/2408.07199)** | arXiv | 2024 | 将规划时的探索轨迹用于策略训练。 | — |
| **[AlphaZero-Like Tree-Search can Guide Large Language Model Decoding and Training](https://proceedings.mlr.press/v235/wan24c.html)** | ICML | 2024 | 将 AlphaZero 式树搜索用于语言模型解码与训练。 | — |
| **[ExACT: Teaching AI Agents to Explore with Reflective-MCTS and Exploratory Learning](https://arxiv.org/abs/2410.02052)** | arXiv | 2024 | 结合反思式树搜索与探索轨迹学习。 | — |
| **[Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models](https://proceedings.mlr.press/v235/zhou24r.html)** | ICML | 2024 | 在树搜索中结合模型判断、环境反馈和反思。 | [GitHub](https://github.com/andyz245/LanguageAgentTreeSearch) [![Stars](https://img.shields.io/github/stars/andyz245/LanguageAgentTreeSearch?style=social&label=Stars)](https://github.com/andyz245/LanguageAgentTreeSearch/stargazers) |
| **[Tree Search for Language Model Agents](https://arxiv.org/abs/2407.01476)** | arXiv | 2024 | 重置环境并重放动作，从而回到先前分支。 | — |

<a name="lookahead"></a>

#### 基于模型的前瞻 (7)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Fact-Augmented Lookahead Planning for LLM Agents](https://proceedings.mlr.press/v300/holt26a.html)** | AISTATS | 2026 | 利用此前回合获得的事实模拟候选动作序列。 | — |
| **[GATS: Graph-Augmented Tree Search with Layered World Models for Efficient Agent Planning](https://arxiv.org/html/2607.08894v1)** | arXiv | 2026 | 在规划中结合符号转移、历史转移统计与模型预测。 | — |
| **[Twin: Playing an Unknown Game with a Test-Time Digital Twin](https://arxiv.org/html/2608.14490v1)** | arXiv | 2026 | 当观测到的状态转移与预测冲突时，修补预测模型。 | [GitHub](https://github.com/Alexyskoutnev/TWIN-ARC-AGI-3) [![Stars](https://img.shields.io/github/stars/Alexyskoutnev/TWIN-ARC-AGI-3?style=social&label=Stars)](https://github.com/Alexyskoutnev/TWIN-ARC-AGI-3/stargazers) |
| **[Plan-and-Act: Improving Planning of Agents for Long-Horizon Tasks](https://proceedings.mlr.press/v267/erdogan25a.html)** | ICML | 2025 | 在长程任务中将生成计划与执行动作分开。 | — |
| **[Test-Time Adaptation for LLM Agents via Environment Interaction](https://arxiv.org/html/2511.04847v4)** | arXiv | 2025 | 通过与目标环境交互调整对环境行为的预测。 | — |
| **[World Model Implanting for Test-time Adaptation of Embodied Agents](https://arxiv.org/html/2509.03956v1)** | arXiv | 2025 | 检索并组合从已有领域学到的世界模型。 | — |
| **[Reasoning with Language Model is Planning with World Model](https://aclanthology.org/2023.emnlp-main.507/)** | EMNLP | 2023 | 用语言模型预测后续推理状态，通过前瞻进行规划。 | — |

---

<a name="adaptation"></a>

### 🧠 基于经验的适应

一次尝试可以留下记忆、技能或模型更新。第 4 章追踪这些变化如何影响后续决策，以及更新规则本身怎样习得。

<a name="memory"></a>

#### 构建记忆 (8)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[AdaMEM: Test-Time Adaptive Memory for Language Agents](https://arxiv.org/html/2606.05684v1)** | arXiv | 2026 | 在执行任务时调整智能体记忆。 | — |
| **[Agentic Memory: Learning Unified Long-Term and Short-Term Memory Management for Large Language Model Agents](https://aclanthology.org/2026.acl-long.981/)** | ACL | 2026 | 学习同时管理短期与长期记忆的策略。 | — |
| **[AgentOCR: Reimagining Agent History via Optical Self-Compression](https://aclanthology.org/2026.acl-long.230/)** | ACL | 2026 | 在单个回合内将交互历史压缩到视觉片段缓存。 | — |
| **[Closing the Feedback Loop: From Experience Extraction to Insight Governance in Verbal Reinforcement Learning](https://arxiv.org/html/2606.17591v1)** | arXiv | 2026 | 追踪针对已有经验总结的反馈。 | — |
| **[Memory-R1: Enhancing Large Language Model Agents to Manage and Utilize Memories via Reinforcement Learning](https://aclanthology.org/2026.acl-long.583/)** | ACL | 2026 | 通过强化学习训练智能体管理和使用记忆。 | — |
| **[Dynamic Cheatsheet: Test-Time Learning with Adaptive Memory](https://arxiv.org/abs/2504.07952v1)** | arXiv | 2025 | 在连续求解过程中整理可复用的文本和代码。 | [GitHub](https://github.com/suzgunmirac/dynamic-cheatsheet) [![Stars](https://img.shields.io/github/stars/suzgunmirac/dynamic-cheatsheet?style=social&label=Stars)](https://github.com/suzgunmirac/dynamic-cheatsheet/stargazers) |
| **[ReasoningBank: Scaling Agent Self-Evolving with Reasoning Memory](https://arxiv.org/abs/2509.25140)** | arXiv | 2025 | 从成功和失败的轨迹中提炼可复用的推理经验。 | [GitHub](https://github.com/google-research/reasoning-bank) [![Stars](https://img.shields.io/github/stars/google-research/reasoning-bank?style=social&label=Stars)](https://github.com/google-research/reasoning-bank/stargazers) |
| **[ExpeL: LLM Agents Are Experiential Learners](https://ojs.aaai.org/index.php/AAAI/article/view/29936)** | AAAI | 2024 | 从已完成的轨迹中提炼经验，用于后续任务。 | [GitHub](https://github.com/LeapLabTHU/ExpeL) [![Stars](https://img.shields.io/github/stars/LeapLabTHU/ExpeL?style=social&label=Stars)](https://github.com/LeapLabTHU/ExpeL/stargazers) |

<a name="retrieval"></a>

#### 检索并使用经验 (9)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Just-In-Time Reinforcement Learning: Continual Learning in LLM Agents Without Gradient Updates](https://proceedings.mlr.press/v306/li26cv.html)** | ICML | 2026 | 根据以往动作的回报调整当前动作分布。 | [GitHub](https://github.com/liushiliushi/JitRL) [![Stars](https://img.shields.io/github/stars/liushiliushi/JitRL?style=social&label=Stars)](https://github.com/liushiliushi/JitRL/stargazers) |
| **[Memex(RL): Scaling Long-Horizon LLM Agents via Indexed Experience Memory](https://arxiv.org/html/2603.04257v1)** | arXiv | 2026 | 为历史经验建立索引，以找回摘要省略的细节。 | — |
| **[MemRL: Self-Evolving Agents via Runtime Reinforcement Learning on Episodic Memory](https://arxiv.org/abs/2601.03192)** | arXiv | 2026 | 先匹配语义相关的记忆，再按估计效用选择。 | [GitHub](https://github.com/MemTensor/MemRL) [![Stars](https://img.shields.io/github/stars/MemTensor/MemRL?style=social&label=Stars)](https://github.com/MemTensor/MemRL/stargazers) |
| **[Reward Is Enough: LLMs Are In-Context Reinforcement Learners](https://arxiv.org/abs/2506.06303)** | ICLR | 2026 | 检验语言模型能否利用上下文奖励调整后续选择。 | — |
| **[SGA-MCTS: Decoupling Planning from Execution via Training-Free Atomic Experience Retrieval](https://aclanthology.org/2026.findings-acl.60/)** | Findings of ACL | 2026 | 检索状态、目标与动作记录，为当前规划提供提示。 | — |
| **[Beyond Numeric Rewards: In-Context Dueling Bandits with LLM Agents](https://aclanthology.org/2025.findings-acl.519/)** | Findings of ACL | 2025 | 研究上下文对决老虎机任务中的偏好反馈。 | — |
| **[In-Context Reinforcement Learning based Retrieval-Augmented Generation for Text-to-SQL](https://aclanthology.org/2025.coling-main.692/)** | COLING | 2025 | 将检索与上下文强化学习用于文本到 SQL 转换。 | — |
| **[Memento: Fine-tuning LLM Agents without Fine-tuning LLMs](https://arxiv.org/abs/2508.16153)** | arXiv | 2025 | 通过相似度或学习得到的 Q 函数为规划器检索案例。 | [GitHub](https://github.com/Memento-Teams/Memento) [![Stars](https://img.shields.io/github/stars/Memento-Teams/Memento?style=social&label=Stars)](https://github.com/Memento-Teams/Memento/stargazers) |
| **[Large Language Models Are Semi-Parametric Reinforcement Learning Agents](https://proceedings.neurips.cc/paper_files/paper/2023/hash/f6b22ac37beb5da61efd4882082c9ecd-Abstract-Conference.html)** | NeurIPS | 2023 | 研究结合已学策略与检索经验的语言模型。 | — |

<a name="skills"></a>

#### 技能与程序 (5)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[APEx: Distillation of Agent Procedural Experience for Adaptive Deep Research Question Answering](https://aclanthology.org/2026.emnlp-main.1105/)** | EMNLP | 2026 | 将轨迹提炼成可用于后续深度研究任务的程序性经验。 | — |
| **[Knowledge is Not Enough: Injecting RL Skills for Continual Adaptation](https://aclanthology.org/2026.acl-long.550/)** | ACL | 2026 | 研究强化学习得到的技能如何支持持续适应。 | — |
| **[Skill-Pro: Learning Reusable Skills from Experience via Non-Parametric PPO for LLM Agents](https://arxiv.org/abs/2602.01869)** | arXiv | 2026 | 规定可复用技能的启动条件，并检查修订方案。 | — |
| **[Skills on the Fly: Test-Time Adaptive Skill Synthesis for LLM Agents](https://arxiv.org/html/2605.16986v2)** | arXiv | 2026 | 在固定求解器执行前，为目标任务构建临时技能。 | — |
| **[Voyager: An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291)** | arXiv | 2023 | 在 Minecraft 中存储可调用和修订的程序技能。 | [GitHub](https://github.com/MineDojo/Voyager) [![Stars](https://img.shields.io/github/stars/MineDojo/Voyager?style=social&label=Stars)](https://github.com/MineDojo/Voyager/stargazers) |

<a name="updates"></a>

#### 模型更新与更新规则 (20)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[A Schema Bounded Language Model for Refining Robot Policies Without Destabilizing Local Learning](https://arxiv.org/html/2609.05133v1)** | arXiv | 2026 | 研究受模式约束的机器人策略修订。 | — |
| **[Agentic ESOpt: Fine-Tuning Long-Horizon LLM Agents with Minimal GPU Requirements](https://arxiv.org/html/2608.17310v2)** | arXiv | 2026 | 研究 GPU 预算受限时长程智能体的策略微调。 | — |
| **[Alpha-RTL: Test-Time Training for RTL Hardware Optimization](https://arxiv.org/abs/2606.05253)** | arXiv | 2026 | 用测试时训练优化寄存器传输级硬件设计。 | — |
| **[Collaborative Multi-Agent Test-Time Reinforcement Learning for Reasoning](https://arxiv.org/abs/2601.09667)** | arXiv | 2026 | 研究多个推理智能体协作时的测试时强化学习。 | — |
| **[From Player to Master: Enhancing Test-Time Learning of LLM Agents via Reinforcement Learning over Memory](https://proceedings.mlr.press/v306/cai26b.html)** | ICML | 2026 | 学习记忆编辑规则，并在留出的对手上评估该规则。 | — |
| **[Learning How and What to Memorize: Cognition-Inspired Two-Stage Optimization for Evolving Memory](https://aclanthology.org/2026.acl-long.2084/)** | ACL | 2026 | 利用反馈学习如何选择和更新记忆。 | — |
| **[Learning to Discover at Test Time](https://arxiv.org/abs/2601.16175)** | arXiv | 2026 | 在针对特定目标搜索产物的过程中更新策略。 | — |
| **[Learning to Learn-at-Test-Time: Language Agents with Learnable Adaptation Policies](https://arxiv.org/abs/2604.00830)** | arXiv | 2026 | 学习适应策略，用来决定智能体应如何更新。 | — |
| **[Learning While Acting: A Skill-Enhanced Test-Time Co-Evolution Framework for Online Lifelong Learning Agents](https://arxiv.org/abs/2606.04815)** | arXiv | 2026 | 利用技能引导的轨迹将行为内化到策略参数。 | — |
| **[On-the-Fly VLA Adaptation via Test-Time Reinforcement Learning](https://aclanthology.org/2026.acl-long.1863/)** | ACL | 2026 | 通过测试时强化学习适应视觉语言动作策略。 | — |
| **[OpenClaw-RL: Train Any Agent Simply by Talking](https://arxiv.org/abs/2603.10165)** | arXiv | 2026 | 使用后续交互中的反馈更新已部署的策略。 | — |
| **[Trust Your Instincts: Confidence-Driven Test-Time RL for Vision-Language-Action Models](https://arxiv.org/html/2606.29892v1)** | arXiv | 2026 | 用置信度指导视觉语言动作模型的测试时强化学习。 | — |
| **[WorldAgen: Unified State-Action Prediction with Test-Time World Model Training](https://arxiv.org/html/2609.08162v1)** | arXiv | 2026 | 使用目标任务中观测到的转移更新世界模型。 | — |
| **[EVOLVE-VLA: Test-Time Training from Environment Feedback for Vision-Language-Action Models](https://arxiv.org/abs/2512.14666)** | arXiv | 2025 | 研究环境反馈与更长的交互轨迹对具身策略适应的影响。 | — |
| **[EvoTest: Evolutionary Test-Time Learning for Self-Improving Agentic Systems](https://arxiv.org/html/2510.13220v2)** | arXiv | 2025 | 在回合之间调整提示词、工具流程与系统设置。 | — |
| **[Learn as Individuals, Evolve as a Team: Multi-agent LLMs Adaptation in Embodied Environments](https://arxiv.org/abs/2506.07232)** | arXiv | 2025 | 研究具身环境中的个体适应与团队适应。 | — |
| **[OPTAGENT: Optimizing Multi-Agent LLM Interactions Through Verbal Reinforcement Learning for Enhanced Reasoning](https://aclanthology.org/2025.findings-ijcnlp.107/)** | Findings of IJCNLP–AACL | 2025 | 通过语言反馈调整多个模型智能体之间的交互。 | — |
| **[Optimizing Test-Time Compute via Meta Reinforcement Finetuning](https://proceedings.mlr.press/v267/qu25g.html)** | ICML | 2025 | 通过元强化微调学习分配测试时计算。 | — |
| **[Self-Improving LLM Agents at Test-Time](https://arxiv.org/html/2510.07841v1)** | arXiv | 2025 | 利用围绕目标输入构建的样例调整模型权重。 | — |
| **[Test-Time Adaptation for Online Vision-Language Navigation with Feedback-based Reinforcement Learning](https://proceedings.mlr.press/v267/kim25ad.html)** | ICML | 2025 | 利用部署阶段的反馈调整视觉语言导航智能体。 | — |

---

<a name="control"></a>

### 🎛️ 自适应改进控制

第 5 章讨论智能体何时投入额外的计算或交互、把资源交给哪个组件，以及何时停止。

<a name="timing"></a>

#### 安排推理与交互 (3)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Timely Machine: Awareness of Time Makes Test-Time Scaling Agentic](https://aclanthology.org/2026.acl-long.211/)** | ACL | 2026 | 在决定行动时机时考虑已经经过的时间。 | — |
| **[Learning When to Plan: Efficiently Allocating Test-Time Compute for LLM Agents](https://arxiv.org/abs/2509.03581)** | arXiv | 2025 | 研究行动前何时值得花费 token 进行规划。 | — |
| **[Thinking vs. Doing: Improving Agent Reasoning by Scaling Test-Time Interaction](https://proceedings.nips.cc/paper_files/paper/2025/hash/f7c4783621a20f5f11a316cd249e0252-Abstract-Conference.html)** | NeurIPS | 2025 | 延长交互时域，比较行动机会与额外推理的作用。 | — |

<a name="allocation"></a>

#### 分配额外计算 (8)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Agentic Test-Time Scaling for WebAgents](https://arxiv.org/html/2602.12276v2)** | arXiv | 2026 | 候选动作出现分歧时触发额外评判。 | — |
| **[Efficient Test-Time Optimization for Multi-Agent Proof Autoformalization](https://arxiv.org/html/2607.11307v1)** | arXiv | 2026 | 用评价准则决定哪些证明分解进入形式验证。 | — |
| **[Inference-Time Budget Control for LLM Search Agents](https://arxiv.org/html/2605.05701v1)** | arXiv | 2026 | 在继续搜索或提交结果时，分别跟踪 token 和工具调用预算。 | — |
| **[PaCoRe: Learning to Scale Test-Time Compute with Parallel Coordinated Reasoning](https://aclanthology.org/2026.acl-long.1253/)** | ACL | 2026 | 通过中间消息协调并行推理轨迹。 | — |
| **[Predicting and improving test-time scaling laws via reward tail-guided search](https://arxiv.org/html/2602.01485v1)** | arXiv | 2026 | 根据奖励分布的尾部指导测试时搜索。 | — |
| **[rSIM: Incentivizing Reasoning Capabilities of LLMs via Reinforced Strategy Injection](https://aclanthology.org/2026.acl-long.2054/)** | ACL | 2026 | 训练模型在推理过程中使用给定策略。 | — |
| **[Scaling Unverifiable Rewards: A Case Study on Visual Insights](https://aclanthology.org/2026.findings-acl.1724/)** | Findings of ACL | 2026 | 按阶段评估视觉推理，把计算集中到需要修订的步骤。 | — |
| **[Multi-Agent Verification: Scaling Test-Time Compute with Multiple Verifiers](https://arxiv.org/html/2502.20379v1)** | arXiv | 2025 | 按预设规模结合多候选采样与多个验证器。 | — |

<a name="routing"></a>

#### 路由与协作 (7)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[MetaAgent-X : Breaking the Ceiling of Automatic Multi-Agent Systems via End-to-End Reinforcement Learning](https://arxiv.org/html/2605.14212v1)** | arXiv | 2026 | 研究如何用端到端强化学习构建多智能体系统。 | — |
| **[Red-Bandit: Test-Time Adaptation for LLM Red-Teaming via Bandit-Guided LoRA Experts](https://aclanthology.org/2026.acl-long.2156/)** | ACL | 2026 | 依据已选专家的响应反馈调整后续专家选择。 | — |
| **[SciToolAgent-Evo: An Ontology-Aware Self-Evolving Agent for Open-World Scientific Tool Acquisition](https://arxiv.org/abs/2607.28692)** | arXiv | 2026 | 根据交互结果选择工具并维护科研工具目录。 | — |
| **[SpatiO: Adaptive Test-Time Orchestration of Vision-Language Agents for Spatial Reasoning](https://arxiv.org/html/2604.21190v3)** | arXiv | 2026 | 在视觉空间推理中组合不同专家的判断。 | — |
| **[Adaptive LLM Routing under Budget Constraints](https://aclanthology.org/2025.findings-emnlp.1301/)** | Findings of EMNLP | 2025 | 在预算约束下为请求选择模型。 | — |
| **[FutureWeaver: Planning Test-Time Compute for Multi-Agent Systems with Modularized Collaboration](https://arxiv.org/html/2512.11213v2)** | arXiv | 2025 | 在预算限制下规划协作模块的调用。 | — |
| **[Learning to Route LLMs from Bandit Feedback: One Policy, Many Trade-offs](https://arxiv.org/html/2510.07429v1)** | arXiv | 2025 | 从老虎机反馈学习适应不同成本偏好的模型路由。 | — |

<a name="stopping"></a>

#### 重试与停止 (1)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[BrowseConf: Confidence-Guided Test-Time Scaling for Web Agents](https://arxiv.org/html/2510.23458v2)** | arXiv | 2025 | 根据模型报告的置信度决定网页智能体是否重试。 | — |

---

<a name="evaluation"></a>

### 📏 评估协议

第 6 章区分不同协议能够支持的结论，包括选择质量、同一任务上的适应、跨任务迁移，以及连续学习。

| 协议 | 比较条件 | 示例 |
| --- | --- | --- |
| 单次执行 | 固定行动模型、候选集合和预算，比较选择机制的贡献。 | [AgentPRM-F](https://arxiv.org/abs/2502.10325) |
| 同一目标上的多次尝试 | 匹配重试次数或成本，并说明最终返回哪次结果。 | [Reflexion](https://proceedings.neurips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html) |
| 留出目标上的迁移 | 分开适应任务与评估目标，记录跨任务保留的状态。 | [MemoPilot](https://proceedings.mlr.press/v306/cai26b.html) |
| 连续任务流 | 按任务顺序记录获取经验的成本及其带来的后续收益。 | [Dynamic Cheatsheet](https://arxiv.org/abs/2504.07952v1) |

<a name="evaluation-search"></a>

#### 搜索、计算与交互预算 (6)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Benchmark Test-Time Scaling of General LLM Agents](https://arxiv.org/abs/2602.18998)** | arXiv | 2026 | 在不同测试时扩展设置下评估通用智能体。 | — |
| **[Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search](https://aclanthology.org/2026.lrec-1.808/)** | LREC | 2026 | 在不同搜索设计和预算下测量准确率与成本。 | — |
| **[SafeSearch: Do Not Trade Safety for Utility in LLM Search Agents](https://aclanthology.org/2026.findings-eacl.146/)** | Findings of EACL | 2026 | 同时考察搜索智能体的安全性与任务效用。 | — |
| **[Guided Search Strategies in Non-Serializable Environments with Applications to Software Engineering Agents](https://proceedings.mlr.press/v267/zainullina25a.html)** | ICML | 2025 | 研究无法任意恢复环境状态时的搜索策略。 | — |
| **[Scaling Test-time Compute for LLM Agents](https://arxiv.org/abs/2506.12928)** | arXiv | 2025 | 研究智能体性能如何随测试时计算量变化。 | — |
| **[When is Tree Search Useful for LLM Planning? It Depends on the Discriminator](https://aclanthology.org/2024.acl-long.738/)** | ACL | 2024 | 研究判别器如何影响树搜索对规划的帮助。 | — |

<a name="evaluation-verification"></a>

#### 验证与反馈可靠性 (8)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Aligning Agents via Planning: A Benchmark for Trajectory-Level Reward Modeling](https://aclanthology.org/2026.acl-long.1062/)** | ACL | 2026 | 评估对完整智能体轨迹给出评分的奖励模型。 | — |
| **[Beyond Majority Voting: Towards Fine-grained and More Reliable Reward Signal for Test-Time Reinforcement Learning](https://aclanthology.org/2026.acl-long.1727/)** | ACL | 2026 | 比较细粒度测试时强化学习奖励信号与多数投票。 | — |
| **[Closing the Reflection Gap: A Free Calibration Bonus for Agentic RL](https://arxiv.org/abs/2606.14211)** | arXiv | 2026 | 研究智能体强化学习中反思判断的校准。 | — |
| **[How Far Are We From True Auto-Research?](https://arxiv.org/html/2605.19156v2)** | arXiv | 2026 | 研究自动化科研中实验产物与论文的评估。 | — |
| **[ToolPRMBench: Evaluating and Advancing Process Reward Models for Tool-using Agents](https://aclanthology.org/2026.findings-acl.602/)** | Findings of ACL | 2026 | 评估工具调用轨迹中的过程奖励模型。 | — |
| **[Understanding and Mitigating Spurious Signal Amplification in Test-Time Reinforcement Learning for Math Reasoning](https://aclanthology.org/2026.findings-acl.1865/)** | Findings of ACL | 2026 | 研究数学推理的测试时强化学习中伪信号的放大。 | — |
| **[Agent-RewardBench: Towards a Unified Benchmark for Reward Modeling across Perception, Planning, and Safety in Real-World Multimodal Agents](https://aclanthology.org/2025.acl-long.857/)** | ACL | 2025 | 评估奖励模型对感知、规划和安全问题的判断。 | — |
| **[Feedback Loops With Language Models Drive In-Context Reward Hacking](https://proceedings.mlr.press/v235/pan24d.html)** | ICML | 2024 | 分析反复反馈下上下文中的奖励投机现象。 | — |

<a name="evaluation-memory"></a>

#### 记忆、迁移与连续任务 (9)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[AgentOdyssey: Open-Ended Long-Horizon Text Game Generation for Test-Time Continual Learning Agents](https://arxiv.org/abs/2606.24893)** | arXiv | 2026 | 生成长程文本游戏，用于评估测试时持续学习。 | — |
| **[AgentStream: How Well Do Self-Evolving LLM Agents Perform Under Streaming Tasks?](https://arxiv.org/abs/2608.00155)** | arXiv | 2026 | 在连续任务流上评估自演化智能体。 | — |
| **[How Memory Management Impacts LLM Agents: An Empirical Study of Experience-Following Behavior](https://aclanthology.org/2026.acl-long.27/)** | ACL | 2026 | 研究记忆管理如何影响智能体对既有经验的依赖。 | — |
| **[Sensi: Learn One Thing at a Time – Curriculum-Based Test-Time Learning for LLM Game Agents](https://arxiv.org/html/2603.17683v1)** | arXiv | 2026 | 利用课程式任务评估游戏智能体的测试时学习。 | — |
| **[The Agent’s First Day: Benchmarking Learning, Exploration, and Scheduling in the Workplace Scenarios](https://aclanthology.org/2026.findings-acl.1505/)** | Findings of ACL | 2026 | 在工作场景中评估学习、探索和任务调度。 | — |
| **[TIDE: Trajectory-based Diagnostic Evaluation of Test-Time Improvement in LLM Agents](https://aclanthology.org/2026.emnlp-main.639/)** | EMNLP | 2026 | 沿轨迹分析完成时间、反复失败和工作记忆。 | — |
| **[When Continual Learning Moves to Memory: A Study of Experience Reuse in LLM Agents](https://arxiv.org/abs/2604.27003)** | arXiv | 2026 | 研究智能体在何种条件下能从经验复用中受益。 | — |
| **[Evo-Memory: Benchmarking LLM Agent Test-time Learning with Self-Evolving Memory](https://arxiv.org/abs/2511.20857)** | arXiv | 2025 | 评估记忆跨任务更新时的测试时学习。 | — |
| **[Minerva: A Programmable Memory Test Benchmark for Language Models](https://proceedings.mlr.press/v267/xia25c.html)** | ICML | 2025 | 分别测试单项记忆操作及其组合。 | — |

---

<a name="background"></a>

### 📖 训练与理论背景

这些工作提供训练方法、奖励设计和理论基础，用于理解正文中的机制比较。

<a name="training"></a>

#### 智能体训练与系统设计 (13)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Claw-R1: A Step-Level Data Middleware System for Agentic Reinforcement Learning](https://arxiv.org/abs/2606.09138v1)** | arXiv | 2026 | 为智能体强化学习提供逐步数据处理组件。 | — |
| **[Closing the Spatial Execution Gap in Digital Whiteboards via Verifiable Reinforcement Learning](https://aclanthology.org/2026.acl-long.630/)** | ACL | 2026 | 用可验证的强化学习反馈训练数字白板上的空间操作。 | — |
| **[CoEvolve: Training LLM Agents via Agent-Data Mutual Evolution](https://aclanthology.org/2026.acl-long.1055/)** | ACL | 2026 | 研究训练数据与智能体协同演化。 | — |
| **[Experience-driven Multi-turn Reinforcement Learning for GUI Agents](https://aclanthology.org/2026.acl-long.428/)** | ACL | 2026 | 利用多轮交互经验训练图形界面智能体。 | — |
| **[MMSearch-R1: Incentivizing LMMs to Search](https://aclanthology.org/2026.acl-long.114/)** | ACL | 2026 | 训练多模态语言模型使用搜索。 | — |
| **[Next-Generation Agentic Reinforcement Learning Systems Enable Self-Evolving Agents](https://arxiv.org/html/2607.01120v2)** | arXiv | 2026 | 讨论持续适应智能体的强化学习系统设计。 | — |
| **[AgentSwift: Efficient LLM Agent Design via Value-guided Hierarchical Search](https://arxiv.org/html/2506.06017v2)** | arXiv | 2025 | 使用价值引导的层次搜索设计智能体。 | — |
| **[Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning](https://arxiv.org/abs/2503.09516)** | arXiv | 2025 | 训练模型在推理过程中使用搜索引擎。 | — |
| **[STAIR: Improving Safety Alignment with Introspective Reasoning](https://proceedings.mlr.press/v267/zhang25cx.html)** | ICML | 2025 | 研究安全对齐训练中的自省推理。 | — |
| **[VLA-RL: Towards Masterful and General Robotic Manipulation with Scalable Reinforcement Learning](https://arxiv.org/abs/2505.18719)** | arXiv | 2025 | 将强化学习用于操作任务中的视觉语言动作模型。 | — |
| **[WebAgent-R1: Training Web Agents via End-to-End Multi-Turn Reinforcement Learning](https://aclanthology.org/2025.emnlp-main.401/)** | EMNLP | 2025 | 基于多轮交互端到端训练网页智能体。 | — |
| **[WebRL: Training LLM Web Agents via Self-Evolving Online Curriculum Reinforcement Learning](https://arxiv.org/abs/2411.02337)** | ICLR | 2025 | 使用随学习过程更新的在线课程训练网页智能体。 | — |
| **[ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)** | ICLR | 2023 | 交替进行推理与行动，并将环境观察用于下一步。 | — |

<a name="rewards"></a>

#### 训练信号与奖励设计 (13)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[ARBOR: Online Process Rewards via a Reusable Rubric Buffer for Search Agents](https://arxiv.org/abs/2606.03239)** | arXiv | 2026 | 维护可复用的评价准则缓冲区，为搜索提供在线过程奖励。 | — |
| **[Chaining the Evidence: Robust Reinforcement Learning for Deep Search Agents with Citation-Aware Rubric Rewards](https://aclanthology.org/2026.acl-long.950/)** | ACL | 2026 | 为深度搜索构建考虑引文证据的评价准则。 | — |
| **[Enhancing LLM-based Search Agents via Contribution Weighted Group Relative Policy Optimization](https://aclanthology.org/2026.acl-long.1462/)** | ACL | 2026 | 在搜索智能体训练中按贡献调整策略优化权重。 | — |
| **[No More Stale Feedback: Co-Evolving Critics for Open-World Agent Learning](https://aclanthology.org/2026.acl-long.576/)** | ACL | 2026 | 使评价器随开放环境中的智能体共同更新。 | — |
| **[Process Reward Models Meet Planning: Generating Precise and Scalable Datasets for Step-Level Rewards](https://aclanthology.org/2026.acl-long.1292/)** | ACL | 2026 | 通过规划生成逐步奖励建模所需的数据集。 | — |
| **[PROGRESS: Coverage-guided RL to Train Search-augmented LLM Agent](https://arxiv.org/html/2608.00969v1)** | arXiv | 2026 | 将覆盖度用作搜索增强智能体的训练信号。 | — |
| **[R-Search: Empowering LLM Reasoning with Search via Multi-Reward Reinforcement Learning](https://aclanthology.org/2026.findings-acl.1896/)** | Findings of ACL | 2026 | 结合多种奖励训练搜索辅助推理。 | — |
| **[Reinforcing Agentic Search Via Reward Density Optimization](https://aclanthology.org/2026.acl-long.467/)** | ACL | 2026 | 在搜索智能体训练中优化奖励密度。 | — |
| **[Search-G1: Co-Evolving Representation-Based Rewards for Selective Grounded Search](https://arxiv.org/html/2608.07531v4)** | arXiv | 2026 | 为有选择地使用外部证据的搜索更新表征奖励。 | — |
| **[Search-P1: Path-Centric Reward Shaping for Stable and Efficient Agentic RAG Training](https://aclanthology.org/2026.acl-industry.36/)** | ACL Industry | 2026 | 按路径为检索增强生成设计奖励。 | — |
| **[SmartSearch: Process Reward-Guided Query Refinement for Search Agents](https://arxiv.org/abs/2601.04888)** | arXiv | 2026 | 用过程奖励指导搜索智能体修订查询。 | — |
| **[SOAR: Supervision from Observation for Agentic Reinforcement Learning](https://aclanthology.org/2026.acl-long.1624/)** | ACL | 2026 | 从智能体的观测中提取训练信号。 | — |
| **[Verified Critical Step Optimization for LLM Agents](https://aclanthology.org/2026.findings-acl.1974/)** | Findings of ACL | 2026 | 针对轨迹中经过验证的关键步骤优化决策。 | — |

<a name="foundations"></a>

#### 理论基础与对照方法 (18)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[Position: Deployed Reinforcement Learning should be Continual](https://arxiv.org/html/2606.04029v2)** | arXiv | 2026 | 讨论部署后继续进行强化学习的必要性。 | — |
| **[Tool Verification for Test-Time Reinforcement Learning](https://arxiv.org/html/2603.02203v2)** | arXiv | 2026 | 使用工具核验测试时强化学习的信号。 | — |
| **[TTVS: Boosting Self-Exploring Reinforcement Learning via Test-time Variational Synthesis](https://aclanthology.org/2026.findings-acl.1634/)** | Findings of ACL | 2026 | 研究通过测试时变分合成进行强化学习探索。 | — |
| **[What If Consensus Lies? Selective-Complementary Reinforcement Learning at Test Time](https://aclanthology.org/2026.acl-long.1337/)** | ACL | 2026 | 研究模型输出形成共识时的选择性与互补学习信号。 | — |
| **[Learning on the Job: Test-Time Curricula for Targeted Reinforcement Learning](https://arxiv.org/abs/2510.04786)** | arXiv | 2025 | 针对特定目标构建测试时课程。 | — |
| **[RL + Transformer = A General-Purpose Problem Solver](https://aclanthology.org/2025.realm-1.29/)** | REALM Workshop | 2025 | 研究结合强化学习的 Transformer 如何求解不同任务。 | — |
| **[Scaling Test-Time Compute Without Verification or RL is Suboptimal](https://proceedings.mlr.press/v267/setlur25a.html)** | ICML | 2025 | 研究缺少验证或强化学习时测试时扩展的局限。 | — |
| **[Test-time Adapted Reinforcement Learning with Action Entropy Regularization](https://proceedings.mlr.press/v267/xu25ar.html)** | ICML | 2025 | 用动作熵正则化支持测试时策略适应。 | — |
| **[Test-Time Graph Search for Goal-Conditioned Reinforcement Learning](https://arxiv.org/abs/2510.07257)** | arXiv | 2025 | 在目标条件强化学习中应用测试时图搜索。 | — |
| **[Towards Provable Emergence of In-Context Reinforcement Learning](https://arxiv.org/abs/2509.18389)** | NeurIPS | 2025 | 分析上下文强化学习出现的条件。 | — |
| **[TTRL: Test-Time Reinforcement Learning](https://proceedings.neurips.cc/paper_files/paper/2025/hash/be690ea16f005c174f6c4102a5970e67-Abstract-Conference.html)** | NeurIPS | 2025 | 研究在测试阶段应用强化学习的方法。 | — |
| **[AMAGO: Scalable In-Context Reinforcement Learning for Adaptive Agents](https://arxiv.org/abs/2310.09971)** | ICLR | 2024 | 研究面向自适应智能体的可扩展上下文强化学习。 | — |
| **[DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models](https://arxiv.org/abs/2402.03300)** | arXiv | 2024 | 研究开放语言模型数学推理中的强化学习。 | — |
| **[In-context Reinforcement Learning with Algorithm Distillation](https://arxiv.org/abs/2210.14215)** | ICLR | 2023 | 将学习历史蒸馏为可在上下文中学习的模型。 | — |
| **[Imitating, Fast and Slow: Robust learning from demonstrations via decision-time planning](https://arxiv.org/abs/2204.03597)** | arXiv | 2022 | 结合示范学习与决策时规划。 | — |
| **[Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347)** | arXiv | 2017 | 提出用于策略学习的近端策略优化算法。 | — |
| **[High-Dimensional Continuous Control Using Generalized Advantage Estimation](https://arxiv.org/abs/1506.02438)** | ICLR | 2016 | 提出用于策略优化的广义优势估计。 | — |
| **[RL^2: Fast Reinforcement Learning via Slow Reinforcement Learning](https://arxiv.org/abs/1611.02779)** | arXiv | 2016 | 通过外层强化学习训练内层学习过程。 | — |

---

<a name="surveys"></a>

### 📚 相关综述

从推理、强化学习和测试时扩展三个角度理解智能体研究。

<a name="survey-papers"></a>

#### 综述论文 (12)

| 论文 | 来源 | 年份 | 简介 | 代码 |
| :--- | :---: | :---: | :--- | :--- |
| **[A Comprehensive Survey of Process Reward Models: Data Generation, Model Construction, and Usage](https://aclanthology.org/2026.acl-long.163/)** | ACL | 2026 | 比较过程奖励模型的数据、训练目标和使用方式。 | — |
| **[A Review on Test-Time Scaling for Agentic Large Language Models](https://ijcai.org/proceedings/2026/859)** | IJCAI | 2026 | 讨论额外的测试时计算如何支持智能体推理和交互。 | — |
| **[A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve on the Path to Artificial Super Intelligence](https://arxiv.org/abs/2507.21046)** | TMLR | 2026 | 按改变的对象、时机和方式梳理自演化智能体。 | — |
| **[A Survey on Self-Improving Test-Time Intelligence: Feedback-Driven Adapting, Learning, and Scaling at Inference](https://arxiv.org/abs/2609.01679)** | arXiv | 2026 | 梳理反馈如何支持推理阶段的适应与额外计算。 | — |
| **[Agentic Reasoning for Large Language Models](https://arxiv.org/abs/2601.12538)** | arXiv | 2026 | 从基础推理、自演化和多智能体协作三个层次梳理智能体推理。 | [GitHub](https://github.com/weitianxin/Awesome-Agentic-Reasoning) [![Stars](https://img.shields.io/github/stars/weitianxin/Awesome-Agentic-Reasoning?style=social&label=Stars)](https://github.com/weitianxin/Awesome-Agentic-Reasoning/stargazers) |
| **[In-Context Reinforcement Learning under Non-Stationarity: A Survey](https://arxiv.org/abs/2607.11906)** | arXiv | 2026 | 梳理环境发生变化时的上下文强化学习。 | — |
| **[When LLM Meets Tree Search: A Systematic View of Inference as Search in Large Language Models](https://arxiv.org/abs/2608.30395)** | arXiv | 2026 | 从树搜索角度比较推理路径的扩展与选择。 | — |
| **[A Comprehensive Survey of Self-Evolving AI Agents: A New Paradigm Bridging Foundation Models and Lifelong Agentic Systems](https://arxiv.org/abs/2508.07407)** | arXiv | 2025 | 讨论基础模型与智能体终身学习的关系。 | — |
| **[A Comprehensive Survey on Learning from Rewards for Large Language Models: Reward Models and Learning Strategies](https://aclanthology.org/2025.findings-emnlp.970/)** | Findings of EMNLP | 2025 | 综述奖励模型及利用其判断进行学习的方法。 | — |
| **[A Survey of In-Context Reinforcement Learning](https://arxiv.org/abs/2502.07978)** | arXiv | 2025 | 综述策略如何从上下文中的交互经验学习。 | — |
| **[The Landscape of Agentic Reinforcement Learning for LLMs: A Survey](https://arxiv.org/abs/2509.02547)** | arXiv | 2025 | 从智能体能力和应用领域梳理强化学习方法。 | [GitHub](https://github.com/HHHHHejia/Awesome-AgenticLLM-RL-Papers) [![Stars](https://img.shields.io/github/stars/HHHHHejia/Awesome-AgenticLLM-RL-Papers?style=social&label=Stars)](https://github.com/HHHHHejia/Awesome-AgenticLLM-RL-Papers/stargazers) |
| **[A survey on large language model based autonomous agents](https://journal.hep.com.cn/fcs/EN/10.1007/s11704-024-40231-1)** | Frontiers of Computer Science | 2024 | 梳理自主智能体的架构、能力获取与评估。 | — |
