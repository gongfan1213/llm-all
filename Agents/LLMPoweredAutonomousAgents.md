- 原文链接：https://lilianweng.github.io/posts/2023-06-23-agent/

# 重点总结

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
