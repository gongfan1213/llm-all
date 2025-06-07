# Day05
---
### 一段话总结  
本文围绕**LangChain与LangGraph的串流技术**展开，介绍了LangChain的`stream`/`astream`方法及事件串流API，通过`StrOutputParser`处理分段输出，并演示如何过滤事件优化效率；LangGraph则支持`values`（完整状态）和`updates`（状态变化）串流模式，可从最终节点串流LLM标记，两者通过分段输出和事件机制提升AI应用的响应速度与灵活性，提供了从基础使用到高级配置的实践案例。

---
### 思维导图  
```mindmap
## **LangChain串流技术**
- 重要性：提升响应速度与用户体验
- 核心方法
  - invoke：生成完整响应后返回
  - stream/astream：分段输出token，返回生成器
  - astream_events/astream_log：串流中间步骤与输出
- 关键组件
  - StrOutputParser：提取chunk内容
  - ChatPromptTemplate：构建提示模板
- 事件流技术
  - 事件类型：on_chat_model_start/stream/end等
  - 过滤技巧：按type/name/tags筛选事件
## **LangGraph串流技术**
- 串流模式
  - values：串流图的完整状态
  - updates：串流状态变化
  - 多模式配置：同时使用values/updates/debug
- 最终节点串流
  - 定义模型与工具：如推荐小吃和饮品的函数
  - 状态图编译：通过StateGraph构建工作流
  - 输出获取：从final节点分段获取结果
## **核心价值**
- 提升用户体验：实时反馈与增量输出
- 开发灵活性：支持多场景配置与细粒度监控
- 性能优化：通过事件过滤减少无效处理
```

---
### 详细总结  

#### **一、LangChain串流技术**  
**1. 串流的重要性**  
- 提升用户体验：通过**分段输出token**实现实时响应，避免完整生成后再返回的延迟。  
- 核心组件支持：聊天模型、输出解析器等均实现`Runnable Interface`，提供`stream`（同步）和`astream`（异步）方法。  

**2. 基础方法：invoke vs stream**  
| 方法       | 特点                          | 示例代码                                                                 |
|------------|-------------------------------|--------------------------------------------------------------------------|
| `invoke()` | 生成完整响应后返回            | `model.invoke("请讲早安问候语")`                                         |
| `stream()` | 分段输出，返回生成器          | `for chunk in model.stream("..."): print(chunk.content)`                  |
| `astream()`| 异步分段输出                  | `async for chunk in model.astream("..."): chunks.append(chunk)`          |

**3. 高级应用：事件串流API**  
- **事件类型**：包括`on_chat_model_start`（模型启动）、`on_chat_model_stream`（token生成）、`on_chat_model_end`（结束）等。  
- **过滤技巧**：通过`include_types`/`include_names`/`include_tags`筛选事件，例如仅监控`chat_model`类型事件：  
  ```python
  async for event in chain.astream_events(..., include_types=["chat_model"]): ...
  ```

**4. 组件整合：Prompt + Model + Parser**  
- 使用`ChatPromptTemplate`构建提示，`StrOutputParser`提取内容，通过`LCEL`（LangChain表达语言）链式组合：  
  ```python
  chain = prompt | model | parser  
  async for chunk in chain.astream({"topic": "父母親"}): print(chunk)  
  ```

#### **二、LangGraph串流技术**  
**1. 串流模式**  
- **`values`模式**：返回图的完整状态，适用于跟踪最终结果。  
  ```python
  async for chunk in graph.astream(inputs, stream_mode="values"):  
      chunk["messages"][-1].pretty_print()  # 显示最新消息  
  ```
- **`updates`模式**：返回节点状态变化，适用于调试。  
  ```python
  async for chunk in graph.astream(inputs, stream_mode="updates"):  
      for node, values in chunk.items(): print(f"节点{node}更新: {values}")  
  ```
- **多模式配置**：同时使用多种模式（如`["values", "updates", "debug"]`）获取全方位数据。  

**2. 最终节点串流**  
- **工作流构建**：通过`StateGraph`定义节点（如`agent`/`tools`/`final`）和状态转移逻辑。  
- **输出获取**：从`final`节点分段获取LLM结果，适用于仅关注最终输出的场景：  
  ```python
  async for chunk in app.astream(inputs, stream_mode="values"):  
      chunk["messages"][-1].pretty_print()  # 输出最终节点的分段结果  
  ```

#### **三、核心价值与实践要点**  
- **用户体验优化**：分段输出让用户感知实时生成，提升交互流畅度。  
- **开发效率提升**：事件流支持细粒度监控（如模型与解析器的独立状态），过滤技术减少无效日志处理。  
- **场景适配**：LangChain适用于单链场景的快速响应，LangGraph适合复杂图结构的多节点协作与状态跟踪。  

---
### 关键问题  
**1. LangChain中stream和invoke的核心区别是什么？**  
- **答案**：`invoke`在模型生成完整响应后返回结果，适用于非实时场景；`stream`以分段形式逐步输出token，返回生成器，可实时展示内容，提升用户体验，适用于需要即时反馈的应用。  

**2. LangGraph的values和updates串流模式有何不同？**  
- **答案**：`values`模式返回图的完整状态（每次节点调用后的全量数据），适合跟踪最终结果；`updates`模式仅返回状态变化（增量数据），适合调试和监控单个节点的行为，两者可按需组合使用。  

**3. 如何利用LangChain的事件串流API优化性能？**  
- **答案**：通过`astream_events`获取详细事件（如模型启动、token生成、解析器输出等），并使用`include_types`/`include_names`/`include_tags`过滤无关事件，减少数据处理量，聚焦关键环节（如仅监控模型生成事件），从而提升性能分析和调试效率。


https://ithelp.ithome.com.tw/articles/10347147





