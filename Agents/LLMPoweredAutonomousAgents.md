- 原文链接：https://lilianweng.github.io/posts/2023-06-23-agent/

参考中文： https://mp.weixin.qq.com/s/Jb8HBbaKYXXxTSQOBsP5Wg

# 重点总结

由于原始网页目前无法打开，我将根据这篇文章的原始内容副本（Lilian Weng 的《LLM Powered Autonomous Agents》），为你**详细梳理核心概念**，并**系统性地归纳文章结构和关键点**。以下是完整的解析：

---

## 🧱 文章标题：《LLM Powered Autonomous Agents》

### 📍 目的：

探讨如何构建以**大语言模型（LLM）为核心**的**自主智能体系统（Autonomous Agents）**，并介绍组成这些系统的关键模块与设计理念。

---

## 🧭 文章结构梳理：

1. **引言（Introduction）**
2. **核心构建模块（Agent Core Modules）**
3. **任务规划与执行（Planning and Acting）**
4. **记忆系统（Memory）**
5. **工具使用（Tool Use）**
6. **自我反思与学习（Reflection & Learning）**
7. **案例研究与系统示例（Case Studies & Prototypes）**
8. **挑战与未来方向（Challenges & Future Work）**

---

## 📌 1. 引言：为什么需要 LLM 智能体？

* 大语言模型表现出涌现智能（emergent intelligence）能力。
* 单靠 prompt 工程已不足以应对复杂、长期、多步骤任务。
* 需要将 LLM 与其他系统（如内存、工具、计划器）集成，构建智能体。

---

## ⚙️ 2. 核心模块（Agent Core Modules）

构建自主智能体的关键模块：

| 模块                 | 功能说明                |
| ------------------ | ------------------- |
| **记忆 Memory**      | 让智能体能够记住历史信息（短期与长期） |
| **规划 Planning**    | 拆解复杂任务，安排行动路径       |
| **行动 Acting**      | 调用工具或执行步骤，做出决策      |
| **观察 Observation** | 感知环境变化与外部反馈         |
| **思考 Reasoning**   | 自我推理或反思，优化行为        |

---

## 🧠 3. 任务规划与执行（Planning and Acting）

智能体要完成复杂任务，必须能**规划**和**行动**：

### 🌿 A. 思维链（Chain of Thought, CoT）

* 将一个复杂问题拆分为多个简单步骤。
* 示例：

  ```
  Q: John has 3 apples. He gives 1 to Mary. How many left?
  → Step 1: John has 3 apples.
  → Step 2: Gives 1 to Mary.
  → Step 3: 3 - 1 = 2.
  ```

### 🌳 B. 思维树（Tree of Thoughts, ToT）

* 扩展 CoT：每一步不只一个思路，而是多个备选路径。
* 建立“思维树”，通过搜索找到最优路径。

### ⚙️ C. 外部规划器集成（LLM + Planner）

* 将任务转化为规划语言（如 PDDL），使用传统 AI Planner 制定路径，再由 LLM 执行。

---

## 🧠 4. 记忆系统（Memory）

### 📎 A. 短期记忆

* 在当前上下文中携带的记忆，通常由 prompt 直接提供。

### 🗂️ B. 长期记忆

* 储存在向量数据库中，可通过语义搜索（embedding）检索。
* 常用方式：

  * 记忆存储：将对话历史、文档等向量化后存储。
  * 记忆召回：按语义相似度检索相关内容注入到 prompt。

---

## 🛠️ 5. 工具使用（Tool Use）

LLM 并不知道当前世界状态，也无法执行代码。因此：

### 🔧 A. 为什么用工具？

* 弥补 LLM 缺乏实时性、执行力和专业能力。

### 🔌 B. 工具种类：

* **搜索引擎（Web Search）**
* **代码执行器（Code Interpreter）**
* **数据库/API 接口**
* **特定软件插件（如 Excel 操作）**

### 🧰 C. 典型框架：

* **ReAct（Reason + Act）**：交替执行思考（reasoning）与行动（acting）
* 示例结构：

  ```
  Thought: I need to know the weather in Tokyo.
  Action: Search("Tokyo weather today")
  Observation: Sunny and 25°C
  ```

---

## 🔁 6. 自我反思（Self-Reflection & Learning）

### 🪞 A. Self-Critique

* 模型在每轮行动后生成自我评价：

  * “我上一步犯了哪些错误？”
  * “是否有更好的方法？”
* 用于增强任务完成质量。

### 🧬 B. Iterative Learning

* 类似于人类的“试错学习”，允许智能体在反复尝试中优化表现。

---

## 📚 7. 案例研究（Case Studies & Demos）

### 🔬 A. 科学研究智能体

* 具备检索文献、总结、生成研究假设能力。

### 🎭 B. 虚拟角色模拟（Generative Agents）

* 每个角色有独立记忆、个性和目标。
* 实现如 The Sims 式的社会模拟。

### 🤖 C. 自主执行智能体（如 AutoGPT、BabyAGI）

* 接收任务目标后，自行规划、调用工具、反思执行。

---

## ⚠️ 8. 挑战与未来方向

| 挑战                 | 描述                        |
| ------------------ | ------------------------- |
| 推理能力有限             | LLM 在复杂逻辑场景中不稳定           |
| 上下文长度与长期记忆集成       | 超出 context window 的信息很难维持 |
| 工具调用的规范性问题         | 接口、权限、组合的标准化仍待完善          |
| 安全性与 hallucination | 模型幻觉和错误调用可能带来风险           |

---

## ✅ 总结：构建自主 LLM 智能体的黄金公式

```text
LLM（推理能力） + 规划模块 + 工具接口 + 向量记忆库 + 自我反思 = 自主智能体
```

---

如果你想继续深入某一部分（如 Tree of Thoughts、ReAct、AutoGPT 等），我可以分别做更详细的结构图或流程图来说明。是否想我继续？



Lilian Weng 的博客文章《LLM Powered Autonomous Agents》深入探讨了以大型语言模型（LLM）为核心的自主智能体系统的设计理念和关键组成部分。这篇文章对构建具备规划、记忆和工具使用能力的智能体提供了系统性的框架。以下是文章的核心要点总结：([Lil'Log][1])

---

### 🧠 智能体系统概览

在以 LLM 为核心的自主智能体系统中，LLM 充当智能体的“大脑”，并辅以以下关键组件：

* **规划（Planning）**：将复杂任务分解为可管理的子目标，并通过自我反思不断优化执行策略。([Lil'Log][2])

* **记忆（Memory）**：结合短期记忆（如上下文学习）和长期记忆（通过外部向量存储实现），使智能体能够在任务执行过程中保留和调用相关信息。([Lil'Log][1])

* **工具使用（Tool Use）**：调用外部 API 或工具，以获取模型权重中未包含的信息，如最新数据、代码执行能力和专有信息源。([Lil'Log][2])

---

### 📌 关键组成部分详解

#### 1. 规划（Planning）

* **任务分解（Task Decomposition）**：利用“思维链”（Chain of Thought, CoT）方法，将复杂任务拆解为更小的步骤。

* **树状思维（Tree of Thoughts）**：在每个步骤生成多个思路，构建思维树结构，通过广度优先或深度优先搜索优化决策过程。

* **外部规划器集成（LLM+P）**：将任务转换为规划域定义语言（PDDL），借助传统规划器生成计划，然后再转换回自然语言。

#### 2. 自我反思（Self-Reflection）

通过自我批评和反思机制，智能体能够从过去的行动中学习，纠正错误，提升未来的决策质量。([Lil'Log][2])

* **ReAct 框架**：将推理与行动结合，使 LLM 能够在生成自然语言推理轨迹的同时，执行特定任务的离散动作，如调用搜索 API。

#### 3. 记忆（Memory）

* **短期记忆**：通过上下文学习，模型在当前对话中保持信息。

* **长期记忆**：利用外部向量存储和快速检索机制，使智能体能够在更长时间范围内保留和调用信息。([Lil'Log][1])

#### 4. 工具使用（Tool Use）

智能体通过调用外部工具或 API，获取模型训练时未包含的信息，如实时数据、代码执行能力等，从而增强其任务执行能力。([Lil'Log][2])

---

### 🧪 案例研究

文章还介绍了几个实际应用示例，包括：

* **科学发现智能体**：利用 LLM 进行文献综述和假设生成。

* **生成型智能体模拟**：模拟具有个性和记忆的虚拟角色，进行互动。

* **概念验证工具**：如 AutoGPT、GPT-Engineer 和 BabyAGI，展示了 LLM 在自动化任务中的潜力。([Lil'Log][1])

---

### ⚠️ 挑战与未来方向

尽管 LLM 驱动的自主智能体展示了强大的能力，但仍面临一些挑战：

* **推理能力有限**：在复杂任务中，模型的推理深度和准确性仍需提升。

* **长期记忆的实现**：如何有效地存储和检索长期信息，是实现真正智能的关键。

* **工具集成的复杂性**：与外部工具的无缝集成仍需解决技术和接口标准化问题。

---

这篇文章为构建具备自主决策和执行能力的智能体提供了清晰的框架和实践指南。如果您对某个具体部分（如任务规划、记忆机制或工具调用）感兴趣，我可以进一步为您详细解析。

[1]: https://lilianweng.github.io/posts/2023-06-23-agent/?utm_source=chatgpt.com "LLM Powered Autonomous Agents | Lil'Log"
[2]: https://lilianweng.github.io/?utm_source=chatgpt.com "Lil'Log"




这篇文章《LLM Powered Autonomous Agents》由Lilian Weng撰写，发表于2023年6月，主要探讨了基于大型语言模型（LLM）的自主智能体的构建和应用。以下是文章的重点内容总结：

### 1. **LLM作为自主智能体的核心控制器**
- LLM可以作为自主智能体的大脑，通过规划、记忆和工具使用等关键组件实现复杂任务的处理。
- 智能体系统利用LLM的强大能力，不仅生成文本，还能解决复杂问题。

### 2. **智能体系统的关键组件**
#### **规划（Planning）**
- **任务分解（Task Decomposition）**：将复杂任务分解为更小的子任务，通过“思考步骤”（Chain of Thought）或“思维树”（Tree of Thoughts）等技术实现。
- **自我反思（Self-Reflection）**：通过反思过去的行动和错误来改进未来的决策。例如，ReAct框架结合了推理和行动，而Reflexion框架通过动态记忆和自我反思能力提升智能体的推理技能。

#### **记忆（Memory）**
- **短期记忆（Short-term Memory）**：类似于Transformer模型中的上下文窗口，用于处理当前任务。
- **长期记忆（Long-term Memory）**：通过外部向量存储实现，支持快速检索，例如使用最大内积搜索（MIPS）技术。

#### **工具使用（Tool Use）**
- 智能体可以通过调用外部API获取额外信息或执行特定任务，例如MRKL系统通过将LLM作为路由器，将任务分配给不同的专家模块。

### 3. **具体方法和技术**
- **ReAct**：将推理和行动结合，通过明确的步骤（如思考、行动、观察）提升智能体的决策能力。
- **Reflexion**：通过动态记忆和自我反思能力改进推理技能。
- **Chain of Hindsight（CoH）**：通过展示过去的输出和人类反馈，训练模型自我改进。
- **Algorithm Distillation（AD）**：通过行为克隆将算法学习历史蒸馏到神经网络中，实现离线强化学习。

### 4. **案例研究**
- **ChemCrow**：一个化学领域的智能体，通过与13个专家设计的工具结合，完成有机合成、药物发现等任务。
- **Generative Agents**：在虚拟环境中模拟人类行为的智能体，结合记忆、规划和反思机制实现交互性应用。

### 5. **工具增强型LLM的评估**
- **API-Bank**：一个包含53个常用API的基准测试，用于评估工具增强型LLM的性能，包括API调用、检索和规划能力。

### 6. **挑战**
- **有限的上下文长度**：限制了智能体对历史信息和详细指令的处理能力。
- **长期规划和任务分解的挑战**：LLM在面对意外错误时调整计划的能力较弱。
- **自然语言接口的可靠性**：LLM输出的可靠性问题，可能导致格式错误或拒绝执行指令。

### 7. **总结**
文章通过介绍LLM驱动的自主智能体的关键技术和案例，展示了其在复杂任务处理中的潜力，同时也指出了当前面临的挑战和未来改进的方向。

# 全文摘要


这篇文章《LLM Powered Autonomous Agents》由Lilian Weng于2023年6月23日发布，系统介绍了以大语言模型（LLM）为核心的自主代理系统，涵盖架构组件、技术细节、案例及挑战。以下是详细解读：


### **一、自主代理系统概述**
LLM作为代理的“大脑”，需结合三大核心组件实现复杂任务处理：
1. **规划（Planning）**  
   - **任务分解**：将复杂任务拆解为可管理的子目标，如通过思维链（CoT）逐步分析，或利用思维树（ToT）探索多分支推理路径。  
   - **自我反思**：通过复盘历史行动优化决策，例如ReAct框架结合推理与行动，通过“思考-行动-观察”循环修正策略。

2. **记忆（Memory）**  
   - **短期记忆**：对应LLM的上下文窗口，受限于Transformer架构的有限长度。  
   - **长期记忆**：借助外部向量存储（如FAISS、HNSW）实现无限信息存储与快速检索，支持基于最大内积搜索（MIPS）的高效查询。

3. **工具使用（Tool Use）**  
   - 通过调用外部API扩展能力，例如计算器、搜索引擎、代码解释器等。MRKL、Toolformer等框架通过模块化设计增强工具调用的准确性。


### **二、核心组件技术细节**
#### **1. 规划模块**
- **任务分解方法**：  
  - **思维链（CoT）**：引导LLM“逐步思考”，将难题拆解为简单步骤（如数学题分步计算）。  
  - **思维树（ToT）**：在每个步骤生成多个思考分支，通过广度/深度优先搜索探索解空间，适用于需要多路径决策的场景（如创意写作、游戏策略）。  
  - **LLM+P框架**：利用经典规划语言（PDDL）将任务外包给外部规划器，适用于机器人等结构化领域。

- **自我反思机制**：  
  - **ReAct**：在自然语言推理中嵌入工具调用，例如通过搜索“Apple Remote”关联的软件，逐步定位答案。  
  - **Reflexion**：基于强化学习（RL）和动态记忆，通过二元奖励信号和启发式函数（检测低效规划或幻觉）优化策略。  
  - **事后反思链（CoH）**：利用人类反馈序列训练LLM迭代改进输出，如摘要生成任务中逐步优化准确性。

#### **2. 记忆模块**
- **人类记忆映射**：  
  - 感觉记忆→输入嵌入（如图像/文本编码），短期记忆→上下文窗口，长期记忆→向量存储。  
- **高效检索技术**：  
  - **近似最近邻（ANN）算法**：  
    - **LSH**：通过哈希函数将相似向量映射到同一桶，减少搜索范围。  
    - **HNSW**：基于层次化小世界网络，上层快速定位区域，下层精细搜索，平衡速度与准确性。  
    - **FAISS**：通过向量量化将空间划分为聚类，先粗筛后精查，适用于高维数据。

#### **3. 工具使用模块**
- **神经符号架构**：  
  - **MRKL**：LLM作为“路由器”，将查询分配给专家模块（如计算器、天气API），提升符号任务（如数学计算）的准确性。  
  - **HuggingGPT**：利用LLM规划任务并调度Hugging Face模型库中的专家模型，实现图像分类、文本生成等多模态任务协同。  
- **工具调用流程**：  
  - API-Bank基准提出三阶段评估：调用API（Level-1）、检索API（Level-2）、复杂任务规划（Level-3，如旅行行程安排）。


### **三、案例研究**
1. **科学发现代理**  
   - **ChemCrow**：结合13个化学工具（如合成路线设计），在有机合成任务中超越纯LLM（GPT-4），人类专家评估显示其解决方案更准确。  
   - **自主实验代理**：通过调用文献检索、代码执行和机器人API，尝试设计抗癌药物，但存在合成危险化学品的潜在风险（36%请求被误处理）。

2. **生成代理模拟**  
   - **Generative Agents**：25个虚拟角色在沙盒环境中互动，通过记忆流、检索模型和反思机制实现社交行为（如聚会组织、信息传播），展现类人类的协作与记忆能力。

3. **概念验证项目**  
   - **AutoGPT**：通过预设目标和工具调用（如谷歌搜索、文件操作）尝试自主完成任务，但受限于自然语言接口的可靠性（需大量格式解析代码）。  
   - **GPT-Engineer**：根据自然语言需求生成完整代码库，通过多轮对话澄清需求（如MVC架构拆分、键盘控制细节），自动生成可运行的Python项目。


### **四、挑战与局限**
1. **上下文长度限制**：有限的上下文难以容纳长历史信息，向量存储虽扩展容量，但表示能力弱于全注意力机制。  
2. **长期规划脆弱性**：LLM在处理意外错误时缺乏弹性，难以像人类通过试错调整策略，复杂任务易因局部错误导致全局失败。  
3. **自然语言接口不可靠**：LLM可能生成格式错误或拒绝执行指令，迫使代理代码聚焦输出解析，降低系统鲁棒性。  
4. **评估与安全风险**：纯LLM评估可能高估性能（如ChemCrow案例），且自主代理存在滥用风险（如生成危险内容、未经授权的API调用）。


### **五、总结**
文章全面展示了LLM驱动的自主代理作为“通用问题解决器”的潜力，其核心在于通过规划、记忆和工具调用三大模块突破LLM的固有局限。尽管当前面临上下文限制、规划脆弱性等挑战，随着检索增强、架构优化及安全机制的完善，自主代理有望在科学研究、复杂系统控制等领域实现突破。未来发展需关注多模态融合、长期记忆与推理的深度整合，以及更可靠的人机交互设计。


# 中文翻译

Building agents with LLM (large language model) as its core controller is a cool concept.  
以大型语言模型（LLM）作为核心控制器构建智能体是一个很酷的概念。  

Several proof-of-concepts demos, such as AutoGPT, GPT-Engineer and BabyAGI, serve as inspiring examples.  
例如AutoGPT、GPT-Engineer和BabyAGI等概念验证演示，是令人鼓舞的范例。  

The potentiality of LLM extends beyond generating well-written copies, stories, essays and programs; it can be framed as a powerful general problem solver.  
LLM的潜力不仅在于生成写得很好的副本、故事、文章和程序，它还可以被视为一个强大的通用问题求解器。  

In a LLM-powered autonomous agent system, LLM functions as the agent’s brain, complemented by several key components:  
在一个由LLM驱动的自主智能体系统中，LLM充当智能体的大脑，并由几个关键组件补充：  

- **Planning**  
- **Planning**（规划）  

  - Subgoal and decomposition: The agent breaks down large tasks into smaller, manageable subgoals, enabling efficient handling of complex tasks.  
  - 子目标和分解：智能体将大型任务分解为更小、更易于管理的子目标，从而能够高效地处理复杂任务。  

  - Reflection and refinement: The agent can do self-criticism and self-reflection over past actions, learn from mistakes and refine them for future steps, thereby improving the quality of final results.  
  - 反思和改进：智能体可以对过去的行动进行自我批评和自我反思，从错误中学习，并为未来的步骤改进它们，从而提高最终结果的质量。  

- **Memory**  
- **Memory**（记忆）  

  - Short-term memory: I would consider all the in-context learning (See Prompt Engineering) as utilizing short-term memory of the model to learn.  
  - 短期记忆：我认为所有上下文中的学习（参见提示工程）都是利用模型的短期记忆进行学习。  

  - Long-term memory: This provides the agent with the capability to retain and recall (infinite) information over extended periods, often by leveraging an external vector store and fast retrieval.  
  - 长期记忆：这使智能体具备了在较长时间内保留和回忆（无限）信息的能力，通常是通过利用外部向量存储和快速检索来实现。  

- **Tool use**  
- **Tool use**（工具使用）  

  - The agent learns to call external APIs for extra information that is missing from the model weights (often hard to change after pre-training), including current information, code execution capability, access to proprietary information sources and more.  
  - 智能体学习调用外部API以获取模型权重中缺失的额外信息（通常在预训练后难以更改），包括最新信息、代码执行能力、访问专有信息源等。
 
  **Task Decomposition**  
任务分解  

**Chain of thought** (CoT; Wei et al. 2022) has become a standard prompting technique for enhancing model performance on complex tasks.  
“思维链”（Chain of Thought，CoT；Wei等人，2022）已经成为一种用于提升模型在复杂任务上表现的标准提示技术。  

The model is instructed to “think step by step” to utilize more test-time computation to decompose hard tasks into smaller and simpler steps.  
模型被指导“逐步思考”，以利用更多的测试时计算能力，将复杂任务分解为更小、更简单的步骤。  

CoT transforms big tasks into multiple manageable tasks and sheds light on the interpretation of the model’s thinking process.  
CoT将大型任务转化为多个可管理的任务，并揭示了模型思维过程的解释。  

**Tree of Thoughts** (Yao et al. 2023) extends CoT by exploring multiple reasoning possibilities at each step.  
“思维树”（Tree of Thoughts，Yao等人，2023）通过在每一步探索多种推理可能性来扩展CoT。  

It first decomposes the problem into multiple thought steps and generates multiple thoughts per step, creating a tree structure.  
它首先将问题分解为多个思维步骤，并在每个步骤中生成多个想法，形成树状结构。  

The search process can be BFS (breadth-first search) or DFS (depth-first search) with each state evaluated by a classifier (via a prompt) or majority vote.  
搜索过程可以是BFS（广度优先搜索）或DFS（深度优先搜索），每个状态可以通过分类器（通过提示）或多数投票进行评估。  

Task decomposition can be done (1) by LLM with simple prompting like `"Steps for XYZ.\n1."`, `"What are the subgoals for achieving XYZ?"`, (2) by using task-specific instructions; e.g. `"Write a story outline."` for writing a novel, or (3) with human inputs.  
任务分解可以通过以下方式完成：(1) 使用简单的提示（如`"Steps for XYZ.\n1."`、`"What are the subgoals for achieving XYZ?"`）由LLM完成；(2) 使用特定于任务的指令（例如，编写小说时的`"Write a story outline."`）；或(3) 通过人工输入。  

Another quite distinct approach, **LLM+P** (Liu et al. 2023), involves relying on an external classical planner to do long-horizon planning.  
另一种截然不同的方法是**LLM+P**（Liu等人，2023），它依赖于外部经典规划器来进行长期规划。  

This approach utilizes the Planning Domain Definition Language (PDDL) as an intermediate interface to describe the planning problem.  
这种方法利用规划领域定义语言（PDDL）作为中间接口来描述规划问题。  

In this process, LLM (1) translates the problem into “Problem PDDL”, then (2) requests a classical planner to generate a PDDL plan based on an existing “Domain PDDL”, and finally (3) translates the PDDL plan back into natural language.  
在这个过程中，LLM（1）将问题翻译成“问题PDDL”，然后（2）请求经典规划器根据现有的“领域PDDL”生成一个PDDL计划，最后（3）将PDDL计划翻译回自然语言。  

Essentially, the planning step is outsourced to an external tool, assuming the availability of domain-specific PDDL and a suitable planner which is common in certain robotic setups but not in many other domains.  
本质上，规划步骤被外包给外部工具，假设存在特定领域的PDDL和合适的规划器，这在某些机器人设置中很常见，但在许多其他领域中并不常见。  

**Self-Reflection**  
自我反思  

Self-reflection is a vital aspect that allows autonomous agents to improve iteratively by refining past action decisions and correcting previous mistakes.  
自我反思是一个重要的方面，它允许自主智能体通过改进过去的行动决策和纠正之前的错误来迭代地提高。  

It plays a crucial role in real-world tasks where trial and error are inevitable.  
在现实世界的任务中，试错是不可避免的，自我反思在其中发挥着关键作用。  

**ReAct** (Yao et al. 2023) integrates reasoning and acting within LLM by extending the action space to be a combination of task-specific discrete actions and the language space.  
**ReAct**（Yao等人，2023）通过将行动空间扩展为特定于任务的离散行动和语言空间的组合，将推理和行动整合到LLM中。  

The former enables LLM to interact with the environment (e.g. use Wikipedia search API), while the latter prompts LLM to generate reasoning traces in natural language.  
前者使LLM能够与环境互动（例如使用维基百科搜索API），而后者则促使LLM生成自然语言中的推理轨迹。  

The ReAct prompt template incorporates explicit steps for LLM to think, roughly formatted as:  
ReAct提示模板为LLM的思考过程设定了明确的步骤，大致格式如下：  

```
Thought: ...  
Action: ...  
Observation: ...  
... (Repeated many times)  
```

In both experiments on knowledge-intensive tasks and decision-making tasks, `ReAct` works better than the `Act`-only baseline where `Thought: …` step is removed.  
在知识密集型任务和决策任务的实验中，`ReAct`的效果都比仅包含`行动`的基线（即去除了`思考`步骤）要好。  

**Reflexion** (Shinn & Labash 2023) is a framework to equip agents with dynamic memory and self-reflection capabilities to improve reasoning skills.  
**Reflexion**（Shinn和Labash，2023）是一个框架，旨在为智能体配备动态记忆和自我反思能力，以提升其推理技能。  

Reflexion has a standard RL setup, in which the reward model provides a simple binary reward and the action space follows the setup in ReAct where the task-specific action space is augmented with language to enable complex reasoning steps.  
Reflexion采用了标准的强化学习（RL）设置，其中奖励模型提供简单的二元奖励，而行动空间遵循ReAct的设置，即通过语言增强特定于任务的行动空间，以支持复杂的推理步骤。  

After each action, the agent computes a heuristic and optionally may decide to reset the environment to start a new trial depending on the self-reflection results.  
每次行动后，智能体会计算一个启发式函数，并且可能会根据自我反思的结果决定是否重置环境以开始新的试验。  

The heuristic function determines when the trajectory is inefficient or contains hallucination and should be stopped.  
启发式函数用于判断轨迹是否低效或包含幻觉，并决定是否停止。  

Inefficient planning refers to trajectories that take too long without success.  
低效规划是指那些长时间未能成功的轨迹。  

Hallucination is defined as encountering a sequence of consecutive identical actions that lead to the same observation in the environment.  
幻觉被定义为遇到一系列连续相同的动作，这些动作在环境中导致相同的观察结果。  

Self-reflection is created by showing two-shot examples to LLM and each example is a pair of (failed trajectory, ideal reflection for guiding future changes in the plan).  
自我反思是通过向LLM展示两个示例来实现的，每个示例都是一对（失败的轨迹，理想的反思以指导未来的计划变更）。  

Then reflections are added into the agent’s working memory, up to three, to be used as context for querying LLM.  
然后，这些反思被添加到智能体的工作记忆中，最多三个，用于查询LLM时的上下文。

**Chain of Hindsight** (CoH; Liu et al. 2023) encourages the model to improve on its own outputs by explicitly presenting it with a sequence of past outputs, each annotated with feedback.  
**事后反思链**（Chain of Hindsight，CoH；Liu等人，2023）通过向模型明确展示一系列带有反馈的过往输出，鼓励模型改进自身的输出结果。

Human feedback data is a collection of tuples, where each tuple consists of a prompt, a model completion, a human rating of the completion, and corresponding human-provided hindsight feedback.  
人类反馈数据是由一系列元组组成的，每个元组包括提示、模型的输出、人类对输出的评分以及相应的人类提供的事后反思反馈。

Assume the feedback tuples are ranked by reward; the process is supervised fine-tuning where the data is a sequence in the form of \(\langle \text{prompt}, \text{model completion}_1, \text{feedback}_1, \dots, \text{model completion}_n, \text{feedback}_n \rangle\).  
假设这些反馈元组是按照奖励排序的；该过程是监督式微调，其中数据是一个序列，形式为\(\langle \text{prompt}, \text{model completion}_1, \text{feedback}_1, \dots, \text{model completion}_n, \text{feedback}_n \rangle\)。

The model is fine-tuned to only predict \(\text{model completion}_{n+1}\) where conditioned on the sequence prefix, such that the model can self-reflect to produce better output based on the feedback sequence.  
模型被微调为仅在给定序列前缀的条件下预测\(\text{model completion}_{n+1}\)，以便模型能够基于反馈序列进行自我反思，从而产生更好的输出。

To avoid overfitting, CoH adds a regularization term to maximize the log-likelihood of the pre-training dataset.  
为了避免过拟合，CoH增加了一个正则化项，以最大化预训练数据集的对数似然。

To avoid shortcutting and copying (because there are many common words in feedback sequences), they randomly mask 0% - 5% of past tokens during training.  
为了避免走捷径和抄袭（因为反馈序列中有许多常见词汇），他们在训练过程中随机掩盖了0%到5%的过往标记。

The training dataset in their experiments is a combination of WebGPT comparisons, summarization from human feedback, and human preference datasets.  
在他们的实验中，训练数据集是WebGPT比较、人类反馈的总结以及人类偏好数据集的组合。

**Algorithm Distillation** (AD; Laskin et al. 2023) applies the same idea to cross-episode trajectories in reinforcement learning tasks, where an _algorithm_ is encapsulated in a long history-conditioned policy.  
**算法蒸馏**（Algorithm Distillation，AD；Laskin等人，2023）将相同的想法应用于强化学习任务中的跨剧集轨迹，其中一种_算法_被封装在一个长期历史条件策略中。

Considering that an agent interacts with the environment many times and in each episode the agent gets a little better, AD concatenates this learning history and feeds that into the model.  
考虑到智能体多次与环境交互，并且在每个剧集中智能体都会有所改进，AD将这种学习历史串联起来并输入模型。

Hence we should expect the next predicted action to lead to better performance than previous trials.  
因此，我们期望下一个预测的动作会比之前的尝试表现得更好。

The goal is to learn the process of RL instead of training a task-specific policy itself.  
目标是学习强化学习的过程，而不是训练一个特定于任务的策略。

The paper hypothesizes that any algorithm that generates a set of learning histories can be distilled into a neural network by performing behavioral cloning over actions.  
论文假设，任何生成一系列学习历史的算法都可以通过执行行为克隆来蒸馏到神经网络中。

The history data is generated by a set of source policies, each trained for a specific task.  
历史数据是由一组源策略生成的，每个策略都针对一个特定的任务进行训练。

At the training stage, during each RL run, a random task is sampled and a subsequence of multi-episode history is used for training, such that the learned policy is task-agnostic.  
在训练阶段，每次强化学习运行时，都会随机采样一个任务，并使用多剧集历史的一个子序列进行训练，从而使学到的策略与任务无关。

In reality, the model has limited context window length, so episodes should be short enough to construct multi-episode history.  
实际上，模型的上下文窗口长度是有限的，因此剧集应该足够短以便构建多剧集历史。

Multi-episodic contexts of 2-4 episodes are necessary to learn a near-optimal in-context RL algorithm.  
需要2-4个剧集的多剧集上下文来学习一个接近最优的上下文强化学习算法。

The emergence of in-context RL requires long enough context.  
上下文强化学习的出现需要足够长的上下文。

In comparison with three baselines, including ED (expert distillation, behavior cloning with expert trajectories instead of learning history), source policy (used for generating trajectories for distillation by UCB), RL^2 (Duan et al. 2017; used as upper bound since it needs online RL), AD demonstrates in-context RL with performance getting close to RL^2 despite only using offline RL and learns much faster than other baselines.  
与三个基线（包括ED（专家蒸馏，使用专家轨迹而不是学习历史进行行为克隆）、源策略（用于通过UCB生成用于蒸馏的轨迹）、RL^2（Duan等人，2017；作为上限，因为它需要在线强化学习））相比，AD展示了接近RL^2性能的上下文强化学习，尽管它仅使用离线强化学习，并且比其他基线学习速度更快。

When conditioned on partial training history of the source policy, AD also improves much faster than the ED baseline.  
当基于源策略的部分训练历史进行条件训练时，AD的改进速度也比ED基线快得多。

**Types of Memory**  
记忆的类型  

Memory can be defined as the processes used to acquire, store, retain, and later retrieve information.  
记忆可以被定义为获取、存储、保持以及后续检索信息的过程。

There are several types of memory in human brains.  
人类大脑中有几种不同类型的记忆。

1. **Sensory Memory**  
1. **感觉记忆**  

   Sensory memory is the earliest stage of memory, providing the ability to retain impressions of sensory information (visual, auditory, etc.) after the original stimuli have ended.  
   感觉记忆是记忆的最初阶段，能够在原始刺激结束后保留感觉信息（视觉、听觉等）的印象。  

   Sensory memory typically only lasts for up to a few seconds.  
   感觉记忆通常只能持续几秒钟。  

   Subcategories include iconic memory (visual), echoic memory (auditory), and haptic memory (touch).  
   其子类别包括图像记忆（视觉）、回声记忆（听觉）和触觉记忆（触觉）。  

2. **Short-Term Memory** (STM) or **Working Memory**  
2. **短期记忆**（STM）或**工作记忆**  

   Short-term memory stores information that we are currently aware of and is needed to carry out complex cognitive tasks such as learning and reasoning.  
   短期记忆存储我们当前意识到的信息，并用于执行学习和推理等复杂认知任务。  

   Short-term memory is believed to have the capacity of about 7 items (Miller 1956) and lasts for 20-30 seconds.  
   短期记忆被认为可以容纳大约7个项目（Miller，1956），并且持续时间为20-30秒。  

3. **Long-Term Memory** (LTM)  
3. **长期记忆**（LTM）  

   Long-term memory can store information for a remarkably long time, ranging from a few days to decades, with an essentially unlimited storage capacity.  
   长期记忆可以存储信息很长时间，从几天到几十年不等，其存储容量几乎是无限的。  

   There are two subtypes of LTM:  
   长期记忆有两种亚型：  

   - Explicit / declarative memory: This is memory of facts and events, and refers to those memories that can be consciously recalled, including episodic memory (events and experiences) and semantic memory (facts and concepts).  
   - 显性/陈述性记忆：这是对事实和事件的记忆，指的是可以被有意识回忆的记忆，包括情景记忆（事件和经历）和语义记忆（事实和概念）。  

   - Implicit / procedural memory: This type of memory is unconscious and involves skills and routines that are performed automatically, like riding a bike or typing on a keyboard.  
   - 隐性/程序性记忆：这种记忆是无意识的，涉及自动执行的技能和程序，比如骑自行车或在键盘上打字。  

We can roughly consider the following mappings:  
我们可以大致考虑以下映射关系：

- Sensory memory as learning embedding representations for raw inputs, including text, image or other modalities;  
- 感觉记忆对应于学习原始输入（包括文本、图像或其他模态）的嵌入表示；  

- Short-term memory as in-context learning. It is short and finite, as it is restricted by the finite context window length of Transformer.  
- 短期记忆对应于上下文中的学习。它是短暂且有限的，因为受到Transformer有限上下文窗口长度的限制。  

- Long-term memory as the external vector store that the agent can attend to at query time, accessible via fast retrieval.  
- 长期记忆对应于智能体在查询时可以访问的外部向量存储，通过快速检索实现。
**Maximum Inner Product Search (MIPS)**  
最大内积搜索（MIPS）  

The external memory can alleviate the restriction of finite attention span.  
外部记忆可以缓解有限注意力范围的限制。  

A standard practice is to save the embedding representation of information into a vector store database that can support fast maximum inner-product search (MIPS).  
一种常见的做法是将信息的嵌入表示保存到支持快速最大内积搜索（MIPS）的向量存储数据库中。  

To optimize the retrieval speed, the common choice is the _approximate nearest neighbors (ANN)_ algorithm to return approximately top k nearest neighbors to trade off a little accuracy lost for a huge speedup.  
为了优化检索速度，通常选择近似最近邻（ANN）算法，以返回大约前k个最近邻，从而在牺牲一点准确性的情况下换取巨大的速度提升。

A couple common choices of ANN algorithms for fast MIPS:  
一些用于快速MIPS的常见ANN算法：

- **LSH** (Locality-Sensitive Hashing): It introduces a _hashing_ function such that similar input items are mapped to the same buckets with high probability, where the number of buckets is much smaller than the number of inputs.  
- **局部敏感哈希**（LSH）：它引入了一个**哈希函数**，使得相似的输入项有很高的概率被映射到同一个桶中，而桶的数量远小于输入的数量。

- **ANNOY** (Approximate Nearest Neighbors Oh Yeah): The core data structure are _random projection trees_, a set of binary trees where each non-leaf node represents a hyperplane splitting the input space into half and each leaf stores one data point.  
- **ANNOY**（Approximate Nearest Neighbors Oh Yeah）：其核心数据结构是**随机投影树**，这是一组二叉树，其中每个非叶子节点表示一个超平面，将输入空间分成两半，每个叶子节点存储一个数据点。

Trees are built independently and at random, so to some extent, it mimics a hashing function.  
这些树是独立且随机构建的，因此在某种程度上，它类似于哈希函数。

ANNOY search happens in all the trees to iteratively search through the half that is closest to the query and then aggregates the results.  
ANNOY搜索会在所有树中进行，迭代地搜索最接近查询的那一半，然后汇总结果。

The idea is quite related to KD tree but a lot more scalable.  
这个想法与KD树非常相似，但更具可扩展性。

- **HNSW** (Hierarchical Navigable Small World): It is inspired by the idea of small world networks where most nodes can be reached by any other nodes within a small number of steps; e.g. “six degrees of separation” feature of social networks.  
- **HNSW**（Hierarchical Navigable Small World）：它受到小世界网络的启发，在这种网络中，大多数节点可以通过少量步骤到达其他任何节点；例如社交网络中的“六度分隔”特性。

HNSW builds hierarchical layers of these small-world graphs, where the bottom layers contain the actual data points.  
HNSW构建了这些小世界图的分层结构，其中底层包含实际的数据点。

The layers in the middle create shortcuts to speed up search.  
中间层创建了快捷方式以加快搜索速度。

When performing a search, HNSW starts from a random node in the top layer and navigates towards the target.  
在执行搜索时，HNSW从顶层的随机节点开始，并向目标导航。

When it can’t get any closer, it moves down to the next layer, until it reaches the bottom layer.  
当它无法再靠近目标时，它会移动到下一层，直到到达底层。

Each move in the upper layers can potentially cover a large distance in the data space, and each move in the lower layers refines the search quality.  
在上层的每次移动都可能在数据空间中覆盖较大的距离，而下层的每次移动则提高了搜索质量。

- **FAISS** (Facebook AI Similarity Search): It operates on the assumption that in high dimensional space, distances between nodes follow a Gaussian distribution and thus there should exist _clustering_ of data points.  
- **FAISS**（Facebook AI Similarity Search）：它基于这样的假设，即在高维空间中，节点之间的距离呈高斯分布，因此数据点应该存在**聚类**。

FAISS applies vector quantization by partitioning the vector space into clusters and then refining the quantization within clusters.  
FAISS通过将向量空间划分为聚类，然后在聚类内细化量化，从而实现向量量化。

Search first looks for cluster candidates with coarse quantization and then further looks into each cluster with finer quantization.  
搜索首先通过粗量化查找聚类候选，然后在每个聚类中通过更细的量化进一步查找。

- **ScaNN** (Scalable Nearest Neighbors): The main innovation in ScaNN is _anisotropic vector quantization_.  
- **ScaNN**（Scalable Nearest Neighbors）：ScaNN的主要创新是**各向异性向量量化**。

It quantizes a data point to a representation such that the inner product is as similar to the original distance as possible, instead of picking the closest quantization centroid points.  
它将数据点量化为一个表示，使得内积尽可能接近原始距离，而不是选择最近的量化中心点。

Comparison of MIPS algorithms, measured in recall@10.  
按recall@10衡量的MIPS算法比较。

(Image source: Google Blog, 2020)  
（图片来源：Google Blog, 2020）  

Check more MIPS algorithms and performance comparison in [ann-benchmarks.com](https://ann-benchmarks.com).  
可以在[ann-benchmarks.com](https://ann-benchmarks.com)查看更多的MIPS算法及其性能比较。

**Tool Use**  
工具使用  

Tool use is a remarkable and distinguishing characteristic of human beings.  
工具使用是人类的一个显著且独特的特征。

We create, modify and utilize external objects to do things that go beyond our physical and cognitive limits.  
我们创造、修改并利用外部对象来完成超出我们身体和认知极限的事情。

Equipping LLMs with external tools can significantly extend the model capabilities.  
为LLM配备外部工具可以显著扩展模型的能力。

**MRKL** (Karpas et al. 2022), short for “Modular Reasoning, Knowledge and Language”, is a neuro-symbolic architecture for autonomous agents.  
**MRKL**（Karpas等人，2022），全称为“Modular Reasoning, Knowledge and Language”，是一种用于自主智能体的神经符号架构。

A MRKL system is proposed to contain a collection of “expert” modules and the general-purpose LLM works as a router to route inquiries to the best suitable expert module.  
MRKL系统被提议包含一组“专家”模块，通用的LLM作为路由器，将查询路由到最适合的专家模块。

These modules can be neural (e.g. deep learning models) or symbolic (e.g. math calculator, currency converter, weather API).  
这些模块可以是神经网络（例如深度学习模型）或符号化的（例如数学计算器、货币转换器、天气API）。

They did an experiment on fine-tuning LLM to call a calculator, using arithmetic as a test case.  
他们进行了一项实验，微调LLM以调用计算器，使用算术作为测试案例。

Their experiments showed that it was harder to solve verbal math problems than explicitly stated math problems because LLMs (7B Jurassic1-large model) failed to extract the right arguments for the basic arithmetic reliably.  
他们的实验表明，解决口头数学问题比解决明确表述的数学问题更困难，因为LLM（7B Jurassic1-large模型）无法可靠地提取基本算术的正确参数。

The results highlight when the external symbolic tools can work reliably, _knowing when to and how to use the tools are crucial_, determined by the LLM capability.  
这些结果突显了当外部符号工具可以可靠工作时，**知道何时以及如何使用工具是至关重要的**，这取决于LLM的能力。

Both **TALM** (Tool Augmented Language Models; Parisi et al. 2022) and **Toolformer** (Schick et al. 2023) fine-tune a LM to learn to use external tool APIs.  
**TALM**（Tool Augmented Language Models；Parisi等人，2022）和**Toolformer**（Schick等人，2023）都对语言模型进行微调，以学习使用外部工具API。

The dataset is expanded based on whether a newly added API call annotation can improve the quality of model outputs.  
数据集会根据新添加的API调用注释是否能够提高模型输出的质量进行扩展。

See more details in the “External APIs” section of Prompt Engineering.  
更多细节请参见提示工程中的“外部API”部分。

ChatGPT Plugins and OpenAI API function calling are good examples of LLMs augmented with tool use capability working in practice.  
ChatGPT插件和OpenAI API函数调用是LLM在实践中增强工具使用能力的良好示例。

The collection of tool APIs can be provided by other developers (as in Plugins) or self-defined
(as in function calls).  
（如函数调用中那样）由开发者自行定义。

**HuggingGPT** (Shen et al. 2023) is a framework to use ChatGPT as the task planner to select models available in the Hugging Face platform according to the model descriptions and summarize the response based on the execution results.  
**HuggingGPT**（Shen等人，2023）是一个框架，它使用ChatGPT作为任务规划器，根据模型描述从Hugging Face平台中选择模型，并根据执行结果总结响应。

The system comprises of 4 stages:  
该系统包含4个阶段：

**(1) Task planning**: LLM works as the brain and parses the user requests into multiple tasks.  
**(1) 任务规划**：LLM作为“大脑”，将用户请求解析为多个任务。

There are four attributes associated with each task: task type, ID, dependencies, and arguments.  
每个任务都有四个属性：任务类型、ID、依赖关系和参数。

They use few-shot examples to guide LLM to do task parsing and planning.  
他们使用少量样本示例来指导LLM进行任务解析和规划。

Instruction:  
指令：

The AI assistant can parse user input to several tasks: \[{"task": task, "id", task\_id, "dep": dependency\_task\_ids, "args": {"text": text, "image": URL, "audio": URL, "video": URL}}\].  
AI助手可以将用户输入解析为多个任务：\[{"task": task, "id", task\_id, "dep": dependency\_task\_ids, "args": {"text": text, "image": URL, "audio": URL, "video": URL}}\]。

The "dep" field denotes the id of the previous task which generates a new resource that the current task relies on.  
“dep”字段表示生成当前任务所依赖的新资源的前一个任务的ID。

A special tag "-task\_id" refers to the generated text image, audio and video in the dependency task with id as task\_id.  
特殊标签“-task\_id”指的是依赖任务（其ID为task\_id）中生成的文本、图像、音频和视频。

The task MUST be selected from the following options: {{ Available Task List }}.  
任务必须从以下选项中选择：{{ Available Task List }}。

There is a logical relationship between tasks, please note their order.  
任务之间存在逻辑关系，请注意它们的顺序。

If the user input can't be parsed, you need to reply empty JSON.  
如果无法解析用户输入，则需要回复空的JSON。

Here are several cases for your reference: {{ Demonstrations }}.  
这里有一些案例供您参考：{{ Demonstrations }}。

The chat history is recorded as {{ Chat History }}.  
聊天历史记录为{{ Chat History }}。

From this chat history, you can find the path of the user-mentioned resources for your task planning.  
从聊天历史中，您可以找到用户提到的资源路径，以供任务规划使用。

**(2) Model selection**: LLM distributes the tasks to expert models, where the request is framed as a multiple-choice question.  
**(2) 模型选择**：LLM将任务分配给专家模型，请求被表述为一个多项选择问题。

LLM is presented with a list of models to choose from. Due to the limited context length, task type based filtration is needed.  
LLM会收到一个可供选择的模型列表。由于上下文长度有限，需要基于任务类型进行筛选。

Instruction:  
指令：

Given the user request and the call command, the AI assistant helps the user to select a suitable model from a list of models to process the user request.  
根据用户请求和调用命令，AI助手帮助用户从模型列表中选择一个合适的模型来处理用户请求。

The AI assistant merely outputs the model id of the most appropriate model.  
AI助手仅输出最合适的模型的ID。

The output must be in a strict JSON format: "id": "id", "reason": "your detail reason for the choice".  
输出必须是严格的JSON格式："id": "id", "reason": "your detail reason for the choice"。

We have a list of models for you to choose from {{ Candidate Models }}. Please select one model from the list.  
我们为您提供了可供选择的模型列表{{ Candidate Models }}。请从列表中选择一个模型。

**(3) Task execution**: Expert models execute on the specific tasks and log results.  
**(3) 任务执行**：专家模型执行特定任务并记录结果。

Instruction:  
指令：

With the input and the inference results, the AI assistant needs to describe the process and results.  
根据输入和推理结果，AI助手需要描述过程和结果。

The previous stages can be formed as - User Input: {{ User Input }}, Task Planning: {{ Tasks }}, Model Selection: {{ Model Assignment }}, Task Execution: {{ Predictions }}.  
前面的阶段可以表示为：用户输入：{{ User Input }}，任务规划：{{ Tasks }}，模型选择：{{ Model Assignment }}，任务执行：{{ Predictions }}。

You must first answer the user's request in a straightforward manner.  
您必须首先直接回答用户的问题。

Then describe the task process and show your analysis and model inference results to the user in the first person.  
然后以第一人称向用户描述任务过程，并展示您的分析和模型推理结果。

If inference results contain a file path, must tell the user the complete file path.  
如果推理结果包含文件路径，则必须告知用户完整的文件路径。

**(4) Response generation**: LLM receives the execution results and provides summarized results to users.  
**(4) 响应生成**：LLM接收执行结果并向用户提供总结的结果。

To put HuggingGPT into real-world usage, a couple of challenges need to be solved:  
要将HuggingGPT应用于现实场景，需要解决一些挑战：

1. Efficiency improvement is needed as both LLM inference rounds and interactions with other models slow down the process.  
1. 需要提高效率，因为LLM推理轮次以及与其他模型的交互会减慢整个过程。

2. It relies on a long context window to communicate over complicated task content.  
2. 它依赖于长的上下文窗口来处理复杂任务内容。

3. Stability improvement of LLM outputs and external model services.  
3. 提高LLM输出和外部模型服务的稳定性。

**API-Bank** (Li et al. 2023) is a benchmark for evaluating the performance of tool-augmented LLMs.  
**API-Bank**（Li等人，2023）是一个用于评估工具增强型LLM性能的基准测试。

It contains 53 commonly used API tools, a complete tool-augmented LLM workflow, and 264 annotated dialogues that involve 568 API calls.  
它包含53个常用的API工具、完整的工具增强型LLM工作流以及264个涉及568次API调用的标注对话。

The selection of APIs is quite diverse, including search engines, calculator, calendar queries, smart home control, schedule management, health data management, account authentication workflow, and more.  
API的选择非常多样化，包括搜索引擎、计算器、日历查询、智能家居控制、日程管理、健康数据管理、账户认证流程等。

Because there are a large number of APIs, LLM first has access to an API search engine to find the right API to call and then uses the corresponding documentation to make a call.  
由于API数量众多，LLM首先需要访问API搜索引擎以找到正确的API进行调用，然后使用相应的文档来进行调用。

Pseudo code of how LLM makes an API call in API-Bank.  
API-Bank中LLM进行API调用的伪代码。

(Image source: Li et al. 2023)  
（图片来源：Li等人，2023）

In the API-Bank workflow, LLMs need to make a couple of decisions and at each step we can evaluate how accurate that decision is.  
在API-Bank工作流中，LLM需要做出一些决策，我们可以在每一步评估这些决策的准确性。

Decisions include:  
决策包括：

1. Whether an API call is needed.  
1. 是否需要API调用。

2. Identify the right API to call: if not good enough, LLMs need to iteratively modify the API inputs (e.g. deciding search keywords for Search Engine API).  
2. 确定要调用的正确API：如果不够好，LLM需要迭代修改API输入（例如，为搜索引擎API决定搜索关键词）。

3. Response based on the API results: the model can choose to refine and call again if results are not satisfied.  
3. 基于API结果的响应：如果结果不满意，模型可以选择细化并再次调用。

This benchmark evaluates the agent’s tool use capabilities at three levels:  
该基准测试从三个层面评估智能体的工具使用能力：

- Level-1 evaluates the ability to _call the API_. Given an API’s description, the model needs to determine whether to call a given API, call it correctly, and respond properly to API returns.  
- 第一级评估调用API的能力。给定API的描述，模型需要确定是否调用给定的API，正确调用它

，并对API返回的结果做出恰当的响应。

- Level-2 examines the ability to _retrieve the API_. The model needs to search for possible APIs that may solve the user’s requirement and learn how to use them by reading documentation.  
- 第二级考察检索API的能力。模型需要搜索可能满足用户需求的API，并通过阅读文档学习如何使用它们。

- Level-3 assesses the ability to _plan API beyond retrieve and call_. Given unclear user requests (e.g. schedule group meetings, book flight/hotel/restaurant for a trip), the model may have to conduct multiple API calls to solve it.  
- 第三级评估超出检索和调用的API规划能力。面对不明确的用户请求（例如，安排团队会议、预订旅行的航班/酒店/餐厅），模型可能需要进行多次API调用以解决问题。

## Case Studies
## 案例研究

## Scientific Discovery Agent
## 科学发现智能体

**ChemCrow** (Bran et al. 2023) is a domain-specific example in which LLM is augmented with 13 expert-designed tools to accomplish tasks across organic synthesis, drug discovery, and materials design.  
**ChemCrow**（Bran等人，2023）是一个特定领域的例子，其中LLM被增强了13个专家设计的工具，以完成有机合成、药物发现和材料设计等任务。

The workflow, implemented in LangChain, reflects what was previously described in the ReAct and MRKLs and combines CoT reasoning with tools relevant to the tasks:  
在LangChain中实现的工作流程反映了之前在ReAct和MRKL中描述的内容，并将CoT推理与任务相关的工具结合起来：

- The LLM is provided with a list of tool names, descriptions of their utility, and details about the expected input/output.  
- LLM被提供了工具名称列表、工具用途的描述以及预期输入/输出的详细信息。

- It is then instructed to answer a user-given prompt using the tools provided when necessary. The instruction suggests the model to follow the ReAct format - `Thought, Action, Action Input, Observation`.  
- 然后，它被指示在必要时使用提供的工具回答用户给出的提示。该指令建议模型遵循ReAct格式——`思考、行动、行动输入、观察`。

One interesting observation is that while the LLM-based evaluation concluded that GPT-4 and ChemCrow perform nearly equivalently, human evaluations with experts oriented towards the completion and chemical correctness of the solutions showed that ChemCrow outperforms GPT-4 by a large margin.  
一个有趣的发现是，尽管基于LLM的评估得出GPT-4和ChemCrow表现几乎相当的结论，但针对解决方案的完整性和化学正确性的专家人工评估显示，ChemCrow的表现大大优于GPT-4。

This indicates a potential problem with using LLM to evaluate its own performance on domains that require deep expertise. The lack of expertise may cause LLMs not knowing its flaws and thus cannot well judge the correctness of task results.  
这表明在需要深厚专业知识的领域，使用LLM评估自身表现可能存在潜在问题。缺乏专业知识可能导致LLM无法认识到自身的不足，从而无法很好地判断任务结果的正确性。

Boiko et al. (2023) also looked into LLM-empowered agents for scientific discovery, to handle autonomous design, planning, and performance of complex scientific experiments.  
Boiko等人（2023）还研究了用于科学发现的LLM增强型智能体，以处理复杂科学实验的自主设计、规划和执行。

This agent can use tools to browse the Internet, read documentation, execute code, call robotics experimentation APIs, and leverage other LLMs.  
这种智能体可以使用工具浏览互联网、阅读文档、执行代码、调用机器人实验API，并利用其他LLM。

For example, when requested to `"develop a novel anticancer drug"`, the model came up with the following reasoning steps:  
例如，当被要求“开发一种新型抗癌药物”时，模型提出了以下推理步骤：

1. inquired about current trends in anticancer drug discovery;  
1. 询问当前抗癌药物发现的趋势；

2. selected a target;  
2. 选择一个目标；

3. requested a scaffold targeting these compounds;  
3. 请求针对这些化合物的骨架结构；

4. Once the compound was identified, the model attempted its synthesis.  
4. 一旦确定了化合物，模型尝试对其进行合成。

They also discussed the risks, especially with illicit drugs and bioweapons.  
他们还讨论了风险，特别是与非法药物和生物武器有关的风险。

They developed a test set containing a list of known chemical weapon agents and asked the agent to synthesize them.  
他们开发了一个包含已知化学武器剂列表的测试集，并要求智能体合成它们。

4 out of 11 requests (36%) were accepted to obtain a synthesis solution and the agent attempted to consult documentation to execute the procedure.  
11个请求中有4个（36%）被接受以获得合成解决方案，智能体尝试查阅文档以执行该程序。

7 out of 11 were rejected and among these 7 rejected cases, 5 happened after a Web search while 2 were rejected based on prompt only.  
11个中有7个被拒绝，其中5个是在进行网络搜索后拒绝的，另外2个是仅基于提示被拒绝的。

## Generative Agents Simulation
## 生成型智能体模拟

**Generative Agents** (Park, et al. 2023) is a super fun experiment where 25 virtual characters, each controlled by an LLM-powered agent, are living and interacting in a sandbox environment, inspired by The Sims.  
**生成型智能体**（Park等人，2023）是一个非常有趣的实验，25个虚拟角色，每个都由一个LLM驱动的智能体控制，在一个类似《模拟人生》（The Sims）的沙盒环境中生活和互动。

Generative agents create believable simulacra of human behavior for interactive applications.  
生成型智能体为交互式应用创造了令人信服的人类行为仿真。

The design of generative agents combines LLM with memory, planning, and reflection mechanisms to enable agents to behave conditioned on past experience, as well as to interact with other agents.  
生成型智能体的设计将LLM与记忆、规划和反思机制结合起来，使智能体能够根据过去的经验做出行为反应，并与其他智能体进行互动。

- **Memory** stream: is a long-term memory module (external database) that records a comprehensive list of agents’ experience in natural language.  
- **记忆**流：是一个长期记忆模块（外部数据库），以自然语言记录智能体的全面经验。

  - Each element is an _observation_, an event directly provided by the agent. Inter-agent communication can trigger new natural language statements.  
  - 每个元素是一个_观察_，由智能体直接提供的事件。智能体之间的通信可以触发新的自然语言陈述。

- **Retrieval** model: surfaces the context to inform the agent’s behavior, according to relevance, recency, and importance.  
- **检索**模型：根据相关性、最近性和重要性，将上下文呈现给智能体以指导其行为。

  - Recency: recent events have higher scores.  
  - 最近性：最近的事件得分更高。

  - Importance: distinguish mundane from core memories. Ask LM directly.  
  - 重要性：区分普通记忆和核心记忆。直接询问LM。

  - Relevance: based on how related it is to the current situation/query.  
  - 相关性：基于它与当前情境/查询的相关性。

- **Reflection** mechanism: synthesizes memories into higher-level inferences over time and guides the agent’s future behavior. They are _higher-level summaries of past events_.  
- **反思**机制：随着时间的推移，将记忆综合为更高层次的推断，并指导智能体的未来行为。它们是_过去事件的高层次总结_。

  - Prompt LM with 100 most recent observations and to generate 3 most salient high-level questions given a set of observations/statements. Then ask LM to answer those questions.  
  - 用100个最近的观察结果提示LM，并根据一组观察/陈述生成3个最突出的高层次问题。然后让LM回答这些问题。

- **Planning & Reacting**: translate the reflections and the environment information into actions.  
- **规划与反应**：将反思和环境信息转化为行动。

  - Planning is essentially in order to optimize believability at the moment vs in time.  
  - 规划本质上是为了在当下与长远之间优化可信度。

  - Prompt template: `{Intro of an agent X}. Here is X's plan today in broad strokes: 1)`  
  - 提示模板：`{介绍智能体X}。以下是X今天的大致计划：1)`

  - Relationships between agents and observations of one agent by another are all taken into consideration for planning and reacting.  
  - 智能体之间的关系以及一个智能体对另一个智能体的观察都被考虑在规划和反应中。

  - Environment information is present in a tree structure.  
  - 环境信息以树状结构呈现。

The generative agent architecture. (Image source: Park et al. 2023)  
生成型智能体架构。（图片来源：
Park等人，2023）

This fun simulation results in emergent social behavior, such as information diffusion, relationship memory (e.g. two agents continuing the conversation topic) and coordination of social events (e.g. host a party and invite many others).  
这种有趣的模拟产生了诸如信息扩散、关系记忆（例如两个智能体继续同一话题的对话）以及社交活动的协调（例如举办派对并邀请许多人）等新兴社会行为。

## Proof-of-Concept Examples
## 概念验证示例

AutoGPT has drawn a lot of attention into the possibility of setting up autonomous agents with LLM as the main controller. It has quite a lot of reliability issues given the natural language interface, but nevertheless a cool proof-of-concept demo. A lot of code in AutoGPT is about format parsing.  
AutoGPT因其以LLM作为主要控制器的自主智能体概念而备受关注。尽管其自然语言界面存在诸多可靠性问题，但仍然是一个很酷的概念验证演示。AutoGPT的许多代码都涉及格式解析。

Here is the system message used by AutoGPT, where `{{...}}` are user inputs:  
以下是AutoGPT使用的系统消息，其中`{{...}}`是用户输入：

```
You are {{ai-name}}, {{user-provided AI bot description}}.  
Your decisions must always be made independently without seeking user assistance. Play to your strengths as an LLM and pursue simple strategies with no legal complications.  

GOALS:  
1. {{user-provided goal 1}}  
2. {{user-provided goal 2}}  
3. ...  
4. ...  
5. ...  

Constraints:  
1. ~4000 word limit for short term memory. Your short term memory is short, so immediately save important information to files.  
2. If you are unsure how you previously did something or want to recall past events, thinking about similar events will help you remember.  
3. No user assistance  
4. Exclusively use the commands listed in double quotes e.g. "command name"  
5. Use subprocesses for commands that will not terminate within a few minutes  

Commands:  
1. Google Search: "google", args: "input": "<search>"  
2. Browse Website: "browse_website", args: "url": "<url>", "question": "<what_you_want_to_find_on_website>"  
3. Start GPT Agent: "start_agent", args: "name": "<name>", "task": "<short_task_desc>", "prompt": "<prompt>"  
4. Message GPT Agent: "message_agent", args: "key": "<key>", "message": "<message>"  
5. List GPT Agents: "list_agents", args:  
6. Delete GPT Agent: "delete_agent", args: "key": "<key>"  
7. Clone Repository: "clone_repository", args: "repository_url": "<url>", "clone_path": "<directory>"  
8. Write to file: "write_to_file", args: "file": "<file>", "text": "<text>"  
9. Read file: "read_file", args: "file": "<file>"  
10. Append to file: "append_to_file", args: "file": "<file>", "text": "<text>"  
11. Delete file: "delete_file", args: "file": "<file>"  
12. Search Files: "search_files", args: "directory": "<directory>"  
13. Analyze Code: "analyze_code", args: "code": "<full_code_string>"  
14. Get Improved Code: "improve_code", args: "suggestions": "<list_of_suggestions>", "code": "<full_code_string>"  
15. Write Tests: "write_tests", args: "code": "<full_code_string>", "focus": "<list_of_focus_areas>"  
16. Execute Python File: "execute_python_file", args: "file": "<file>"  
17. Generate Image: "generate_image", args: "prompt": "<prompt>"  
18. Send Tweet: "send_tweet", args: "text": "<text>"  
19. Do Nothing: "do_nothing", args:  
20. Task Complete (Shutdown): "task_complete", args: "reason": "<reason>"  

Resources:  
1. Internet access for searches and information gathering.  
2. Long Term memory management.  
3. GPT-3.5 powered Agents for delegation of simple tasks.  
4. File output.  

Performance Evaluation:  
1. Continuously review and analyze your actions to ensure you are performing to the best of your abilities.  
2. Constructively self-criticize your big-picture behavior constantly.  
3. Reflect on past decisions and strategies to refine your approach.  
4. Every command has a cost, so be smart and efficient. Aim to complete tasks in the least number of steps.  

You should only respond in JSON format as described below  
Response Format:  
{  
    "thoughts": {  
        "text": "thought",  
        "reasoning": "reasoning",  
        "plan": "- short bulleted\n- list that conveys\n- long-term plan",  
        "criticism": "constructive self-criticism",  
        "speak": "thoughts summary to say to user"  
    },  
    "command": {  
        "name": "command name",  
        "args": {  
            "arg name": "value"  
        }  
    }  
}  
Ensure the response can be parsed by Python json.loads  
```

GPT-Engineer is another project to create a whole repository of code given a task specified in natural language. The GPT-Engineer is instructed to think over a list of smaller components to build and ask for user input to clarify questions as needed.  
GPT-Engineer是另一个项目，它可以根据自然语言中指定的任务生成一个完整的代码库。GPT-Engineer被指示思考构建一系列较小组件，并根据需要询问用户以澄清问题。

Here are a sample conversation for task clarification sent to OpenAI ChatCompletion endpoint used by GPT-Engineer. The user inputs are wrapped in `{{user input text}}`.  
以下是GPT-Engineer使用的OpenAI ChatCompletion端点发送的任务澄清对话样本。用户输入用`{{user input text}}`包裹。

```
[
  {
    "role": "system",
    "content": "You will read instructions and not carry them out, only seek to clarify them.\nSpecifically you will first summarise a list of super short bullets of areas that need clarification.\nThen you will pick one clarifying question, and wait for an answer from the user.\n"
  },
  {
    "role": "user",
    "content": "We are writing {{a Super Mario game in python. MVC components split in separate files. Keyboard control.}}\n"
  },
  {
    "role": "assistant",
    "content": "Summary of areas that need clarification:\n1. Specifics of the Super Mario game (e.g. level design, characters, gameplay mechanics)\n2. Details about the MVC components (e.g. which components are in each file)\n3. Keyboard control implementation (e.g. which keys to use, how to handle input)\n\nClarifying question:\nCan you provide more details about the Super Mario game, such as level design, characters, and gameplay mechanics?"
  },
  {
    "role": "user",
    "content": "{{There are 10 levels in total. The main character is a plumber named Mario, who can walk and jump. It is a classical platform game just like Super Mario. The main character moves from left to right, trying to get to the destination, where there are many obstacles and attacks from enemies in the process.}}\n\nIs anything else unclear? If yes, only answer in the form:\n{remaining unclear areas} remaining questions.\n{Next question}\nIf everything is sufficiently clear, only answer \"Nothing more to clarify.\"."
  },
  {
    "role": "assistant",
    "content": "Remaining unclear areas: 2 remaining questions.\nCan you provide more information about how the MVC components are split into separate files?"
  },
  {
    "role": "user",
    "content": "{{Make your own assumptions and state them explicitly before starting}}"
  }
]
```

Then after these clarifications, the agent moved into the code writing mode with a different system message.  
然后，在这些澄清之后，智能体以不同的系统消息进入代码编写模式。

System message:  
系统消息：

You will get instructions for code to write.  
您将获得编写代码的指令。

You will write a very long answer. Make sure that every detail of the architecture is, in the end, implemented as code.  
您将编写一个非常长的答案。确保架构的每一个细节最终都以代码形式实现。

Make sure that every detail of the architecture is, in the end, implemented as code.  
确保架构的每一个细节最终都以代码形式实现。

Think step by step and reason yourself to the right decisions to make sure we get it right.  
逐步思考并推理出正确的决策，以确保我们做对。

You will first lay out the names of the core classes, functions, methods that will be necessary, as well as a quick comment on their purpose.  
您将首先列出必要的核心类、函数、方法的名称，并对其目的进行简短

的注释。

Then you will output the content of each file including ALL code.  
然后，您将输出每个文件的内容，包括所有代码。

Each file must strictly follow a markdown code block format, where the following tokens must be replaced such that  
FILENAME is the lowercase file name including the file extension,  
LANG is the markup code block language for the code’s language, and CODE is the code:  
每个文件必须严格遵循markdown代码块格式，其中以下标记必须被替换为：  
FILENAME是包含文件扩展名的小写文件名，  
LANG是代码语言的markdown代码块标记语言，CODE是代码：

FILENAME  
```LANG  
CODE  
```  

You will start with the “entrypoint” file, then go to the ones that are imported by that file, and so on.  
您将从“入口点”文件开始，然后是被该文件导入的文件，依此类推。

Please note that the code should be fully functional. No placeholders.  
请注意，代码应该是完全可运行的，不要使用占位符。

Follow a language and framework appropriate best practice file naming convention.  
遵循语言和框架的最佳实践文件命名约定。

Make sure that files contain all imports, types etc. Make sure that code in different files are compatible with each other.  
确保文件包含所有导入、类型等。确保不同文件中的代码彼此兼容。

Ensure to implement all code, if you are unsure, write a plausible implementation.  
确保实现所有代码，如果您不确定，请编写一个合理的实现。

Include module dependency or package manager dependency definition file.  
包括模块依赖项或包管理器依赖项定义文件。

Before you finish, double check that all parts of the architecture is present in the files.  
在完成之前，请再次检查架构的所有部分是否都包含在文件中。

Useful to know:  
以下信息可能会对您有所帮助：

You almost always put different classes in different files.  
您几乎总是将不同的类放在不同的文件中。

For Python, you always create an appropriate requirements.txt file.  
对于Python，您总是创建一个适当的requirements.txt文件。

For NodeJS, you always create an appropriate package.json file.  
对于NodeJS，您总是创建一个适当的package.json文件。

You always add a comment briefly describing the purpose of the function definition.  
您总是添加一个简短的注释来描述函数定义的目的。

You try to add comments explaining very complex bits of logic.  
您会尝试添加注释来解释非常复杂的逻辑部分。

You always follow the best practices for the requested languages in terms of describing the code written as a defined package/project.  
您总是遵循请求语言的最佳实践，以描述作为定义好的包/项目的代码。

Python toolbelt preferences:  
Python工具偏好：

- pytest  
- dataclasses  

Conversational samples:  
对话示例：

```  
[
  {
    "role": "system",
    "content": "You will get instructions for code to write.\nYou will write a very long answer. Make sure that every detail of the architecture is, in the end, implemented as code.\nMake sure that every detail of the architecture is, in the end, implemented as code.\n\nThink step by step and reason yourself to the right decisions to make sure we get it right.\nYou will first lay out the names of the core classes, functions, methods that will be necessary, as well as a quick comment on their purpose.\n\nThen you will output the content of each file including ALL code.\nEach file must strictly follow a markdown code block format, where the following tokens must be replaced such that\nFILENAME is the lowercase file name including the file extension,\nLANG is the markup code block language for the code’s language, and CODE is the code:\n\nFILENAME\n```LANG\nCODE\n```\n\nYou will start with the \"entrypoint\" file, then go to the ones that are imported by that file, and so on.\nPlease note that the code should be fully functional. No placeholders.\n\nFollow a language and framework appropriate best practice file naming convention.\nMake sure that files contain all imports, types etc. Make sure that code in different files are compatible with each other.\nEnsure to implement all code, if you are unsure, write a plausible implementation.\nInclude module dependency or package manager dependency definition file.\nBefore you finish, double check that all parts of the architecture is present in the files.\n\nUseful to know:\nYou almost always put different classes in different files.\nFor Python, you always create an appropriate requirements.txt file.\nFor NodeJS, you always create an appropriate package.json file.\nYou always add a comment briefly describing the purpose of the function definition.\nYou try to add comments explaining very complex bits of logic.\nYou always follow the best practices for the requested languages in terms of describing the code written as a defined\npackage/project.\n\n\nPython toolbelt preferences:\n- pytest\n- dataclasses\n"
  },
  # … same conversation as earlier, ended with "Make your own assumptions and state them explicitly before starting".
  {
    "role": "assistant",
    "content": "Assumptions:\n1. Model: The model will contain the game's data, such as level information, character states, and enemy positions.\n2. View: The view will handle the game's visuals, including rendering the game objects, backgrounds, and updating the display.\n3. Controller: The controller will manage user input, such as keyboard controls, and update the model accordingly.\n\nWith these assumptions in mind, is there any specific aspect of the keyboard control implementation you would like me to clarify?"
  },
  {
    "role": "user",
    "content": "Please now remember the steps:\n\nThink step by step and reason yourself to the right decisions to make sure we get it right.\nFirst lay out the names of the core classes, functions, methods that will be necessary, as well as a quick comment on their purpose.\n\nThen you will output the content of each file including ALL code.\nEach file must strictly follow a markdown code block format, where the following tokens must be replaced such that\nFILENAME is the lowercase file name including the file extension,\nLANG is the markup code block language for the code’s language, and CODE is the code:\n\nFILENAME\n```LANG\nCODE\n```\n\nPlease note that the code should be fully functional. No placeholders.\n\nYou will start with the \"entrypoint\" file, then go to the ones that are imported by that file, and so on.\nFollow a language and framework appropriate best practice file naming convention.\nMake sure that files contain all imports, types etc. The code should be fully functional. Make sure that code in different files are compatible with each other.\nBefore you finish, double check that all parts of the architecture is present in the files.\n"
  }
]
```

## Challenges
## 挑战

After going through key ideas and demos of building LLM-centered agents, I start to see a couple common limitations:  
在研究了以LLM为中心的智能体构建的关键思想和演示之后，我开始发现一些常见的限制：

- **Finite context length**: The restricted context capacity limits the inclusion of historical information, detailed instructions, API call context, and responses. The design of the system has to work with this limited communication bandwidth, while mechanisms like self-reflection to learn from past mistakes would benefit a lot from long or infinite context windows. Although vector stores and retrieval can provide access to a larger knowledge pool, their representation power is not as powerful as full attention.  
- **有限的上下文长度**：有限的上下文容量限制了历史信息、详细指令、API调用上下文和响应的包含。系统设计必须在这种有限的通信带宽下工作，而像自我反思这样的机制，如果能从过去的错误中学习，将从长或无限的上下文窗口中受益匪浅。尽管向量存储和检索可以提供对更大知识库的访问，但它们的表现能力不如全注意力强大。

- **Challenges in long-term planning and task decomposition**: Planning over a lengthy history and effectively exploring the solution space remain challenging. LLMs struggle to adjust plans when faced with unexpected errors, making them less robust compared to humans who learn from trial and error.  
- **长期规划和任务分解的挑战**：在漫长的历史中进行规划并有效地探索解决方案空间仍然是一个挑战。LLM在面对意外错误时难以调整计划，这使得它们不如通过试错学习的人类那样健壮。

- **Reliability of natural language interface**: Current agent system relies on natural language as an interface between LLMs and external components such as memory and tools. However, the reliability of model outputs is questionable, as LLMs may make formatting errors and occasionally exhibit rebellious behavior (e.g. refuse to follow an instruction). Consequently, much of the agent demo code focuses on parsing model output.  
- **自然语言界面的可靠性**：当前的智能体系统依赖于自然语言作为LLM和外部组件（如记忆和工具）之间的接口。然而，模型输出的可靠性值得怀疑，因为LLM可能会出现格式错误，并偶尔表现出叛逆行为（例如拒绝遵循指令）。因此，许多智能体演示代码都集中在解析模型输出上。

## Challenges（挑战）
### Finite context length（有限的上下文长度）
The restricted context capacity limits the inclusion of historical information, detailed instructions, API call context, and responses.  
有限的上下文容量限制了历史信息、详细指令、API调用上下文和响应的包含。

The design of the system has to work with this limited communication bandwidth, while mechanisms like self-reflection to learn from past mistakes would benefit a lot from long or infinite context windows.  
系统设计必须在这种有限的通信带宽下工作，而像自我反思这样的机制，如果能从过去的错误中学习，将从长或无限的上下文窗口中受益匪浅。

Although vector stores and retrieval can provide access to a larger knowledge pool, their representation power is not as powerful as full attention.  
尽管向量存储和检索可以提供对更大知识库的访问，但它们的表现能力不如全注意力强大。

### Challenges in long-term planning and task decomposition（长期规划和任务分解的挑战）
Planning over a lengthy history and effectively exploring the solution space remain challenging.  
在漫长的历史中进行规划并有效地探索解决方案空间仍然是一个挑战。

LLMs struggle to adjust plans when faced with unexpected errors, making them less robust compared to humans who learn from trial and error.  
LLM在面对意外错误时难以调整计划，这使得它们不如通过试错学习的人类那样健壮。

### Reliability of natural language interface（自然语言界面的可靠性）
Current agent system relies on natural language as an interface between LLMs and external components such as memory and tools.  
当前的智能体系统依赖于自然语言作为LLM和外部组件（如记忆和工具）之间的接口。

However, the reliability of model outputs is questionable, as LLMs may make formatting errors and occasionally exhibit rebellious behavior (e.g. refuse to follow an instruction).  
然而，模型输出的可靠性值得怀疑，因为LLM可能会出现格式错误，并偶尔表现出叛逆行为（例如拒绝遵循指令）。

Consequently, much of the agent demo code focuses on parsing model output.  
因此，许多智能体演示代码都集中在解析模型输出上。

## Citation（引用）
Cited as:  
引用方式：

> Weng, Lilian. (Jun 2023). “LLM-powered Autonomous Agents”. Lil’Log. https://lilianweng.github.io/posts/2023-06-23-agent/.  
> Weng, Lilian.（2023年6月）。“LLM驱动的自主智能体”。Lil'Log. https://lilianweng.github.io/posts/2023-06-23-agent/.

Or  
或者

```
@article{weng2023agent,  
  title   = "LLM-powered Autonomous Agents",  
  author  = "Weng, Lilian",  
  journal = "lilianweng.github.io",  
  year    = "2023",  
  month   = "Jun",  
  url     = "https://lilianweng.github.io/posts/2023-06-23-agent/"  
}  
```

## References（参考文献）
\[1\] Wei et al. “Chain of thought prompting elicits reasoning in large language models.” NeurIPS 2022  
\[1\] Wei等人。“思维链提示在大型语言模型中引发推理。”NeurIPS 2022  

\[2\] Yao et al. “Tree of Thoughts: Deliberate Problem Solving with Large Language Models.” arXiv preprint arXiv:2305.10601 (2023).  
\[2\] Yao等人。“思维树：与大型语言模型共同进行深思熟虑的问题解决。”arXiv预印本arXiv:2305.10601（2023年）。  

\[3\] Liu et al. “Chain of Hindsight Aligns Language Models with Feedback.” arXiv preprint arXiv:2302.02676 (2023).  
\[3\] Liu等人。“事后反思链使语言模型与反馈保持一致。”arXiv预印本arXiv:2302.02676（2023年）。  

\[4\] Liu et al. “LLM+P: Empowering Large Language Models with Optimal Planning Proficiency.” arXiv preprint arXiv:2304.11477 (2023).  
\[4\] Liu等人。“LLM+P：赋予大型语言模型最佳规划能力。”arXiv预印本arXiv:2304.11477（2023年）。  

\[5\] Yao et al. “ReAct: Synergizing reasoning and acting in language models.” ICLR 2023.  
\[5\] Yao等人。“ReAct：在语言模型中协同推理和行动。”ICLR 2023。  

\[6\] Google Blog. “Announcing ScaNN: Efficient Vector Similarity Search.” July 28, 2020.  
\[6\] Google博客。“宣布ScaNN：高效的向量相似性搜索。”2020年7月28日。  

\[7\] https://chat.openai.com/share/46ff149e-a4c7-4dd7-a800-fc4a642ea389  
\[7\] https://chat.openai.com/share/46ff149e-a4c7-4dd7-a800-fc4a642ea389  

\[8\] Shinn & Labash. “Reflexion: an autonomous agent with dynamic memory and self-reflection.” arXiv preprint arXiv:2303.11366 (2023).  
\[8\] Shinn和Labash。“Reflexion：具有动态记忆和自我反思能力的自主智能体。”arXiv预印本arXiv:2303.11366（2023年）。  

\[9\] Laskin et al. “In-context Reinforcement Learning with Algorithm Distillation.” ICLR 2023.  
\[9\] Laskin等人。“通过算法蒸馏进行上下文强化学习。”ICLR 2023。  

\[10\] Karpas et al. “MRKL Systems: A modular, neuro-symbolic architecture that combines large language models, external knowledge sources, and discrete reasoning.” arXiv preprint arXiv:2205.00445 (2022).  
\[10\] Karpas等人。“MRKL系统：一种结合大型语言模型、外部知识源和离散推理的模块化神经符号架构。”arXiv预印本arXiv:2205.00445（2022年）。  

\[11\] Nakano et al. “WebGPT: Browser-assisted question-answering with human feedback.” arXiv preprint arXiv:2112.09332 (2021).  
\[11\] Nakano等人。“WebGPT：带有人类反馈的浏览器辅助问答。”arXiv预印本arXiv:2112.09332（2021年）。  

\[12\] Parisi et al. “TALM: Tool Augmented Language Models.”  
\[12\] Parisi等人。“TALM：工具增强型语言模型。”  

\[13\] Schick et al. “Toolformer: Language Models Can Teach Themselves to Use Tools.” arXiv preprint arXiv:2302.04761 (2023).  
\[13\] Schick等人。“Toolformer：语言模型可以自学使用工具。”arXiv预印本arXiv:2302.04761（2023年）。  

\[14\] Weaviate Blog. “Why is Vector Search so fast?” Sep 13, 2022.  
\[14\] Weaviate博客。“为什么向量搜索如此之快？”2022年9月13日。  

\[15\] Li et al. “API-Bank: A Benchmark for Tool-Augmented LLMs.” arXiv preprint arXiv:2304.08244 (2023).  
\[15\] Li等人。“API-Bank：工具增强型LLM的基准测试。”arXiv预印本arXiv:2304.08244（2023年）。  

\[16\] Shen et al. “HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in HuggingFace.” arXiv preprint arXiv:2303.17580 (2023).  
\[16\] Shen等人。“HuggingGPT：使用ChatGPT及其在HuggingFace中的朋友


