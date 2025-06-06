https://github.com/Heng-xiu/agentic-system-lab-2024ironman

# 什麼是 AI 代理？複合式 AI 與 Agentic AI 的創新之路
本文围绕AI代理与复合式AI系统展开，探讨从单一模型到智能代理的技术演进，核心内容如下：


### **一、单一模型的局限与复合式AI系统的兴起**
- **案例引入**：智慧打卡系统需同时处理影像辨识（员工进出记录）和数据库查询（剩余假期），单一模型（如仅用影像辨识模型）无法满足多任务需求。
- **复合式AI系统定义**：由多个互动组件（如大语言模型、检索器、外部工具）协同处理任务的系统，例如：
  - **检索增强系统（RAG）**：结合大语言模型推理与资料检索生成回答。
  - **对话式AI**：具备上下文记忆，可处理复杂查询（如结合RAG的客服系统）。
  - **人机协作工具（CoPilots）**：深度适配用户工作环境，如MetaGPT自动生成研究报告、Devin辅助编程。
- **优势**：
  - **模块化设计**：组件可独立替换（如图像模型、数据库接口），便于系统调整。
  - **灵活性**：可整合外部资源（如实时数据、权限系统），突破单一模型训练数据的限制。
  - **高效解决企业问题**：通过组合工具提升应用质量，避免单纯依赖大模型的“收益递减”问题。


### **二、AI代理（AI Agent）的核心概念**
- **定义**：以语言模型为驱动，具备自主解决问题能力的系统，核心能力包括：
  1. **思考分析**：分解复杂任务为可执行步骤（如将“规划旅行”拆解为“查机票→订酒店→设计行程”）。
  2. **规划能力**：制定从当前状态到目标状态的路径（如根据用户预算和时间规划最优路线）。
  3. **工具运用**：调用外部工具（如地图API、天气查询）完成任务。
  4. **信息保存**：存储对话历史或中间结果，提供连贯的个性化交互（如记住用户偏好的酒店类型）。
- **运作模式**：基于**ReAct框架**，流程为：  
  **接收任务→分析并规划步骤→调用工具执行→验证结果是否达标→未达标则重复流程**。
- **与传统聊天机器人的区别**：
  | **特征**         | **聊天机器人**                | **AI代理**                  |
  |------------------|-----------------------------|---------------------------|
  | **决策自主性**   | 依赖预设规则/脚本，无法自主决策 | 独立评估情境，自主规划行动      |
  | **情境感知**     | 仅基于当前对话，忽略用户情绪/偏好 | 理解对话上下文、情绪及历史互动   |
  | **学习能力**     | 无法从互动中学习              | 持续优化决策能力              |
  | **多模态支持**   | 仅限文本交互                  | 支持文字、语音、图像等多模态输入 |


### **三、从Agent到Agentic的认知升级**
- **概念区分**：
  - **Agent**：名词，指具备特定功能的独立实体（如专注于数据分析的代理）。
  - **Agentic**：形容词，描述系统具备类似代理的特性（如自主性、规划能力），是一个连续的能力光谱（而非非此即彼）。
- **意义**：推动AI系统从“被动执行指令”向“主动解决问题”进化，例如：
  - 传统聊天机器人仅能按预设脚本回答“营业时间”，而Agentic系统可自主整合实时数据、用户历史偏好，推荐个性化服务。


### **四、应用案例：智慧打卡系统的Agentic实现**
1. **任务拆解**：
   - 影像辨识：通过摄像头捕捉员工面部特征，调用图像模型识别身份。
   - 考勤记录：识别成功后自动记录时间，存入数据库。
   - 假期查询：根据员工ID调用人事系统API，返回剩余假期天数。
2. **复合式架构**：
   - 大语言模型（LLM）：解析用户查询意图（如“查询我的假期”），规划任务步骤（先查ID→再查数据库）。
   - 图像模型：处理员工辨识任务。
   - 数据库接口：执行假期数据查询。


### **五、未来趋势与思考**
- **技术方向**：
  - 更深度的工具整合（如机器人控制、物联网设备）。
  - 强化长期记忆与跨任务迁移能力（如代理可将办公场景的规划能力迁移至家庭场景）。
- **应用潜力**：
  - 企业流程自动化（如财务报销、供应链管理）。
  - 个人助理（如健康管理、教育辅导）。
- **挑战**：需平衡自主性与可控性，避免代理执行不可预期的行为。


### **总结**
复合式AI系统与AI代理标志着AI从“单一模型时代”迈向“智能协作时代”。AI代理通过整合大语言模型的推理能力、多工具协同及自主决策，能够高效解决复杂任务，未来将在企业与个人场景中释放巨大潜力。
# LangGraph：構建下一代智能應用的革命性框架


---
### 一段话总结  
**LangGraph是一个基于图结构的复合式AI系统开发框架**，将AI代理抽象为图节点、代理间通信为边，通过**状态管理**维护上下文连贯，**协调能力**确保任务顺序执行，兼容LangChain生态。其核心优势包括简化复杂工作流程、提升开发效率，适用于智能客服、流程自动化、多代理协作等场景，但需注意学习曲线和性能优化问题。

---
### 思维导图  
```mindmap
## **核心概念**
- 图结构：节点（代理）、边（信息传递）
- 状态管理：维护上下文、追踪关键信息
- 协调能力：任务排序、代理间信息交换
## **应用场景**
- 智能客服：多LLM代理处理查询
- 工作流程自动化：文档处理、审批流程
- 多代理协作：供应链管理、同步决策
- 智能推荐系统：用户行为分析、精准推荐
- 个性化学习平台：学习进度评估、定制反馈
## **使用步骤**
- 环境准备：安装langgraph、langchain等库
- 定义状态：通过StateGraph构建状态机
- 定义语言模型：初始化LLM（如ChatOpenAI）
- 添加节点：将代理功能注册为图节点
- 构建与编译图：设置入口/结束节点并编译
- 实现交互：循环处理用户输入与代理响应
## **优势与挑战**
- 优势：简化开发、结构化框架、灵活状态管理、多代理协调
- 挑战：学习曲线、性能优化、数据安全与隐私
```

---
### 详细总结  

#### 一、LangGraph的定位与核心特性  
**LangGraph是基于LangChain扩展的复合式AI系统开发框架**，专为构建**状态化、多代理协作应用**设计，核心特性包括：  
1. **图结构建模**：  
   - 将AI代理抽象为**有向图节点**，代理间信息传递为**边**，清晰描述工作流程（如客服系统中不同代理处理不同查询类型）。  
   - 示例：智能客服中，“意图识别代理”节点接收用户输入，通过边将信息传递给“知识库查询代理”节点。  
2. **状态管理**：  
   - 维护代理执行任务时的实时状态（如对话历史、中间结果），确保上下文连贯。  
   - 应用：在多轮对话中追踪用户偏好，避免重复询问信息。  
3. **任务协调**：  
   - 自动管理代理执行顺序和数据流，开发者只需关注业务逻辑（如先调用图像识别代理，再调用数据查询代理）。  

#### 二、应用场景与典型案例  
| **场景**         | **应用方式**                                                                 | **优势**                          |  
|------------------|-----------------------------------------------------------------------------|-----------------------------------|  
| **智能客服**     | 多LLM代理分别处理业务咨询、投诉等，状态管理保持对话主题连贯                 | 支持复杂查询，提升用户体验        |  
| **工作流程自动化** | 代理自动处理文档审核、数据录入、审批流程，状态管理记录流程进度               | 减少人工干预，降低错误率          |  
| **多代理协作**   | 供应链管理中，库存代理、物流代理、订单代理通过图结构协同决策                 | 提升系统响应速度和运营效率        |  
| **智能推荐系统** | 多代理分析用户行为、偏好数据，整合多数据源生成推荐                          | 精准匹配用户需求，提升转化率      |  
| **个性化学习平台** | 代理评估学生表现，状态管理记录学习进度，动态调整学习内容                     | 实现定制化教育，提高学习效率      |  

#### 三、快速上手：聊天机器人开发示例  
1. **环境搭建**：  
   ```bash  
   pip install langgraph langchain langchain-openai  
   ```  
2. **代码实现关键步骤**：  
   - **定义状态**：用`StateGraph`管理对话历史（`messages`字段）。  
     ```python  
     from langgraph.graph import StateGraph  
     class State(TypedDict):  
         messages: list  # 存储对话消息列表  
     ```  
   - **初始化LLM**：使用OpenAI的GPT-4模型。  
     ```python  
     from langchain_openai import ChatOpenAI  
     llm = ChatOpenAI(model="gpt-4-0613", temperature=0)  
     ```  
   - **构建图结构**：将聊天功能注册为节点，并设置为入口/结束点。  
     ```python  
     graph_builder = StateGraph(State)  
     graph_builder.add_node("chatbot", lambda state: {"messages": [llm.invoke(state["messages"])])  
     graph_builder.set_entry_point("chatbot").set_finish_point("chatbot")  
     ```  
   - **交互循环**：处理用户输入并生成响应。  
     ```python  
     while True:  
         user_input = input("用户: ")  
         if user_input.lower() in ["quit", "exit"]: break  
         for event in graph.stream({"messages": [("user", user_input)]}):  
             print("AI助理:", event.values()[0]["messages"][-1].content)  
     ```  

#### 四、优势与挑战  
- **核心优势**：  
  - **开发效率高**：抽象底层细节，聚焦业务逻辑（如无需手动管理代理通信）。  
  - **结构清晰**：图结构使系统流程可视化，便于团队协作和维护。  
  - **灵活性强**：支持动态扩展代理节点，适应需求变化（如新增支付代理）。  
- **面临挑战**：  
  - **学习门槛**：需理解图结构、状态管理等新概念，对新手不友好。  
  - **性能优化**：大规模场景下，代理间通信和状态存储可能影响响应速度。  
  - **隐私安全**：处理敏感数据时，需额外设计权限控制和加密机制。  

---  
### 关键问题与答案  
1. **LangGraph与LangChain的区别是什么？**  
   **答案**：LangChain是基础的LLM应用开发框架，侧重单模型交互；**LangGraph是其扩展框架**，引入图结构和多代理协作能力，专门解决复合式AI系统的开发复杂度问题，支持状态管理和代理间协调。  

2. **状态管理在LangGraph中的具体作用是什么？**  
   **答案**：状态管理用于维护代理执行任务时的上下文信息（如对话历史、任务进度），确保多轮交互中系统行为连贯。例如在智能客服中，状态管理可记录用户之前咨询的订单号，避免重复询问。  

3. **LangGraph适用于哪些类型的企业场景？**  
   **答案**：适用于需要多环节协作的复杂场景，例如：  
   - **跨部门流程自动化**（如报销审批：票据识别代理→财务审核代理→领导审批代理）；  
   - **实时数据处理**（如电商推荐：用户行为分析代理→库存查询代理→推荐生成代理）；  
   - **多语言客服**（不同语言代理节点根据用户输入自动切换）。
  
# LangGraph 入門教程：節點、邊、狀態

该网页是《2024 年用 LangGraph 从零开始实现 Agentic AI System》系列文的第 4 篇，主要介绍 LangGraph 的核心元件（节点、边、状态）及如何用它们构建简单的天气查询代理，具体内容如下：

### **一、LangGraph 概述**
- **定位**：由 LangChain 团队开发，用于构建更灵活、复杂的 AI 代理工作流程，是 LangChain 的扩展套件。
- **核心思想**：将工作流程可视化为由**节点**（任务）和**边**（任务间连接，定义执行顺序和条件）组成的图形，配备**共享状态系统**传递信息，解决传统 LangChain 处理复杂交互工作流的不足（如线性执行模式难以应对条件分支、循环和并行任务，跨步骤状态维护困难等）。

### **二、LangChain 与 LangGraph 的关键区别**
|**比较项目**|**LangChain**|**LangGraph**|
|----|----|----|
|工作流结构|主要是线性的，适合顺序执行的任务|基于图的结构，适合复杂、非线性的工作流|
|灵活性|在处理条件分支和循环时较为受限|可以轻松定义条件路径、循环和并行任务|
|状态管理|在跨多个步骤维护状态时可能遇到困难|提供了一个共享的状态系统，方便在整个工作流中传递信息|
|可视化|工作流程可能不太直观|将工作流可视化為图，使复杂系统更易于理解和设计|
|使用场景|适合相对简单、直接的 AI 任务|适合需要复杂决策和多路径执行的高级 AI 系统|

### **三、LangGraph 的核心元件**
1. **图形（Graph）**：LangGraph 的核心，包含所有节点和它们之间的连接，是工作流程的整体架构，类似路线图。
2. **状态（State）**：
    - 是捕获应用程序当前快照的共享数据结构，可存储整个过程中的重要信息，每个节点都可读写，类型通常是 TypedDict 或 Pydantic BaseModel。
    - 有**基本图**（只能传递节点输出，无状态）和**有状态图**（可包含状态，节点间可传递状态）两种类型。
3. **节点（Node）**：图中的各个站点，代表特定任务或检查点，如同工作流程中的专业人员，接收输入、处理并产出输出，可执行简单数据转换或复杂决策等操作。
4. **边（Edge）**：连接节点的路径，决定信息在节点间的流动及条件，包括：
    - **普通边**：直接连接两个节点，指定节点输出作为另一节点输入，用`add_edge('node_1', 'node_2')`添加。
    - **入口点和终点**：入口点（START）是图开始执行的第一个节点，终点（END）是结束节点，用`add_edge(START, "node_a")` `add_edge("node_2", END)`设置。
    - **条件边**：根据特定条件选择下一个执行的节点，用`add_conditional_edges('agent', where_to_go, {"end": END, "continue": "weather_tool"})`添加，其中`where_to_go`是条件判断函数。

### **四、实战应用：构建天气查询 Agent**
1. **定义状态**：创建存储对话消息的状态`AllState`，用 TypedDict 定义包含`messages`键，值为字符串列表，使用`operator.add`作为 reducer 组合消息。
    ```python
    from typing import TypedDict, Annotated, Sequence
    import operator
    class AllState(TypedDict):
        messages: Annotated[Sequence[str], operator.add]
    ```
2. **创建节点**：
    - **提取城市节点（agent）**：使用 LangChain 的模型和提示模板从用户查询中提取城市名。
        ```python
        from langchain_openai import ChatOpenAI
        from langchain.prompts import ChatPromptTemplate
        model = ChatOpenAI(temperature=0.4)
        prompt_str = """你收到一个问题，需要从中提取城市名称。除城市名称外不要回复任何内容，如果找不到城市名称就不回复。如果存在城市名称，只回复城市名称；如果问题中没有城市名称，就回复'no_response'。问题：{user_query}"""
        prompt = ChatPromptTemplate.from_template(prompt_str)
        chain = prompt | model
        def call_model(state: AllState):
            messages = state["messages"]
            response = chain.invoke(messages)
            return {"messages": [response]}
        ```
    - **天气查询节点（weather）**：模拟根据城市名查询天气的函数，真实场景可接 OpenWeather API。
        ```python
        def get_taiwan_weather(city: str) -> str:
            weather_data = {"台北": "晴天，温度28°C", "台中": "多云，温度26°C", "高雄": "阴天，温度30°C"}
            return f"{city}的天气：{weather_data.get(city, '暂无资料')}"
        def weather_tool(state):
            context = state["messages"]
            city_name = context[1].content
            data = get_taiwan_weather(city_name)
            return {"messages": [data]}
        ```
    - **响应节点（responder）**：用模型根据用户查询和天气信息生成响应。
        ```python
        response_prompt_str = """你收到一条天气信息，需要根据该信息回复用户的查询。用户查询：---{user_query}--- 信息：---{information}---"""
        response_prompt = ChatPromptTemplate.from_template(response_prompt_str)
        response_chain = response_prompt | model
        def responder(state: AllState):
            messages = state["messages"]
            response = response_chain.invoke({"user_query": messages[0], "information": messages[1]})
            return {"messages": [response]}
        ```
3. **连接节点（构建图）**：
    - 添加节点到图中。
        ```python
        graph_builder = StateGraph(AllState)
        graph_builder.add_node("agent", call_model)
        graph_builder.add_node("weather", weather_tool)
        graph_builder.add_node("responder", responder)
        ```
    - 添加边，设置入口点和终点，处理条件情况（如用户查询无城市名时结束流程）。
        ```python
        def query_classify(state: AllState):
            messages = state["messages"]
            ctx = messages[1].content  # 提取城市名的响应
            if ctx == "no_response":
                return "end"  # 无城市名，结束
            else:
                return "continue"  # 有城市名，继续查询天气
        graph_builder.add_conditional_edges("agent", query_classify, {"end": END, "continue": "weather"})
        graph_builder.add_edge("weather", "responder")
        graph_builder.add_edge("responder", END)
        graph_builder.set_entry_point("agent")
        graph_builder.set_finish_point(END)
        ```
4. **编译并执行图**：
    ```python
    app = graph_builder.compile()
    # 模拟用户输入
    user_query = "台北今天天气如何？"
    for event in app.stream({"messages": [user_query]}):
        for value in event.values():
            print("AI 回应:", value["messages"][-1])
    ```

### **五、总结**
- **核心价值**：通过节点、边和状态三大核心元件，LangGraph 提供了模块化、可视化的复杂工作流构建方式，提升了 AI 系统的灵活性、可扩展性和可维护性。
- **未来展望**：文中期待后续探索 LangGraph 的更多进阶应用场景，进一步发挥其在构建智能系统中的潜力，推动 AI 技术创新发展。

- # LangChain 與 LangGraph 串流技術深度探索

-    
