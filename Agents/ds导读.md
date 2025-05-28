以下是学习AI Agents（人工智能代理）时推荐的必读论文，涵盖基础理论、架构设计、应用案例及前沿研究。这些论文来自权威机构（如微软、谷歌、MetaGPT等）和顶级会议（如NeurIPS、ICLR、AAAI等），帮助你全面掌握AI Agents的核心技术与最新进展：

---

### **一、基础理论与架构设计**
1. **《The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey》**  
   - **作者**：IBM & 微软研究人员（2024）  
   - **内容**：全面分析AI Agent在推理、规划和工具调用方面的架构设计，对比单智能体与多智能体系统的优劣，探讨如何通过角色定义和动态协作提升性能。  
   - **重点**：适合理解Agent的核心工作机制，如任务分解、多计划选择和记忆增强规划。

2. **《Advances and Challenges in Foundation Agents: From Brain-Inspired Intelligence to Evolutionary, Collaborative, and Safe Systems》**  
   - **作者**：MetaGPT、微软、港科大、斯坦福等20家机构联合发表（2025）  
   - **内容**：264页综述，从认知科学、神经科学角度分析AI Agents的模块化设计（如记忆、世界模型、奖励系统），并探讨自我进化与多Agent协作机制。  
   - **重点**：适合研究受大脑启发的Agent架构和长期学习能力。

3. **《Sibyl: Simple yet Effective Agent Framework for Complex Real-world Reasoning》**  
   - **作者**：Sibyl团队（2024）  
   - **内容**：提出一个基于全球工作空间理论和心智理论的Agent框架，通过多主体辩论提升复杂推理能力，在GAIA基准测试中表现优异。  
   - **重点**：适合关注现实世界任务（如金融分析、决策支持）的研究者。

---

### **二、多智能体系统（Multi-Agent Systems, MAS）**
4. **《PEER: Expertizing Domain-Specific Tasks with a Multi-Agent Framework and Tuning Methods》**  
   - **作者**：PEER团队（2024）  
   - **内容**：提出PEER（规划-执行-表达-审查）多Agent框架，优化专业领域任务（如金融问答）的性能，成本仅为GPT-4的5%，同时保障数据隐私。  
   - **重点**：适合研究垂直领域（医疗、法律、金融）的Agent优化。

5. **《BMW Agents: A Framework for Task Automation Through Multi-Agent Collaboration》**  
   - **作者**：BMW研究团队（2024）  
   - **内容**：探讨工业场景下多Agent协作的自动化框架，适用于知识检索、机器人流程自动化（RPA）等复杂任务。  
   - **重点**：适合企业级自动化应用（如供应链、制造）。

6. **《AutoAgents: Automated Agent Generation Framework》**  
   - **作者**：北京大学陈光耀团队（2023）  
   - **内容**：提出无需预定义角色的动态Agent生成方法，通过“起草-执行”两阶段优化多Agent协作效率。  
   - **重点**：适合研究Agent自动生成与自适应学习。

---

### **三、应用与行业实践**
7. **《Agentic Workflow: 25篇智能体工作流论文综述》**  
   - **作者**：王吉伟（2024）  
   - **内容**：总结吴恩达提出的四种Agentic Workflow设计模式（反思、工具使用、规划、多Agent协作），并分析Coze、文心智能体等平台的实践案例。  
   - **重点**：适合研究工作流自动化（如客服、内容生成）。

8. **《企业内部规模化AI Agents应用与实践用例》**  
   - **作者**：杨芳贤（2025）  
   - **内容**：解析企业如何部署AI Agents（如Klarna的客服Agent节省4000万美元），涵盖单Agent与多Agent编排模式，以及安全护栏设计。  
   - **重点**：适合企业技术负责人或AI产品经理。

9. **《无信任自主性：理解自主权去中心化AI代理的动机、益处和治理困境》**  
   - **作者**：胡博涛、刘宇涵等（2025）  
   - **内容**：探讨区块链+AI Agents的结合（如DeAgents），分析去中心化治理与可靠性挑战。  
   - **重点**：适合研究Web3、DAO、DeFi等领域的AI应用。

---

### **四、前沿研究方向**
10. **《LLM Powered Autonomous Agents》**  
    - **作者**：Lilian Weng（OpenAI前首席安全研究员）  
    - **内容**：经典论文，定义AI Agents的四大核心能力（感知-分析-决策-执行），并探讨记忆模块与工具调用的设计。  
    - **重点**：适合入门Agent基础理论。

11. **《Humanoid Agents: Simulating Human-like Generative Agents》**  
    - **作者**：英伟达王智琳团队（2023）  
    - **内容**：基于马斯洛需求层次理论构建类人Agent，模拟人类行为与心理状态变化。  
    - **重点**：适合研究社交模拟、游戏NPC、虚拟人。

12. **《Towards the Era of Agents: A Survey on Large Language Model-Based Agents》**  
    - **作者**：MetaGPT团队（2024）  
    - **内容**：系统梳理LLM-based Agents的发展历程，从单Agent到多Agent社会，并讨论评估标准与伦理问题。  

---

### **如何获取这些论文？**
- 部分论文可在arXiv（如[PEER](https://arxiv.org/abs/2407.06985)、[BMW Agents](https://arxiv.org/abs/2406.20041)）或会议官网（如NeurIPS、ICLR）下载。  
- 打包资源：在微信公众号【会议之眼】回复“AI-Agents”获取23篇精选论文，或访问[未来知识库](https://wx.zsxq.com/group/454854145828)获取更多综述。

---

### **学习建议**
1. **从基础到进阶**：先读Lilian Weng的《LLM Powered Autonomous Agents》和IBM/微软的架构综述，再深入研究多Agent系统（如AutoAgents、PEER）。  
2. **结合实践**：参考企业内部应用案例（如Klarna、摩根士丹利）理解Agent落地的挑战。  
3. **关注趋势**：去中心化AI（DeAgents）和受神经科学启发的Agent设计是当前热点。  

如果需要更具体的领域（如医疗、金融、游戏）论文推荐，可以进一步说明！
