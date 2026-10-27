# project1_reactagent
# 🧠 从零手写 ReAct 智能体核心循环 (Pure Python ReAct Loop)

## 📖 项目简介

本项目是 AI Agent 开发的最底层、最纯粹的实战演练（Project V0）。
在没有使用任何第三方 Agent 框架（如 LangChain、AutoGen 等）的情况下，本项目使用**纯 Python 代码**，利用最基础的 `while` 循环和 `openai` 官方 SDK，硬核还原了 AI Agent 的 **ReAct（Reasoning and Acting，推理与行动）** 核心机制。

**核心价值**：彻底撕开大模型“黑盒”，弄懂大模型是如何通过文本输出（Thought/Action）来反向控制代码流程的。

## ✨ 核心亮点

1. **纯手写任务循环**：利用 `for step in range(max_steps)` 模拟 Agent 的思考循环，打破“一问一答”的单轮限制。
2. **格式约束与正则解析**：通过严苛的 System Prompt 约束大模型输出格式，并通过 Python 的 `re`（正则表达式）模块，精准提取大模型的意图（如提取 `Thought` 和 `Final Answer`）。
3. **初探长期记忆**：代码预留了 Redis 连接，尝试将多轮对话的 `messages` 序列化存入数据库，实现持久化上下文。
4. **接入 DeepSeek API**：兼容 OpenAI 接口协议，大幅降低大模型调用成本。

## 🛠️ 环境依赖

由于本项目是最纯粹的基础脚本，仅依赖少量的网络与数据处理库。

```bash
pip install openai redis

在终端执行以下指令启动：

bash
python react_agent.py

测试一：测试它能不能正常对话
text
你好，我叫小明，我最喜欢的数字是 7，请记住。
测试二：测试它的“短期记忆”（看看 Redis 起没起效）
text
你还记得我叫什么名字吗？我最喜欢的数字是几？
(如果它回答出了小明和7，说明它成功读取了 Redis 里的历史记忆)

测试三：测试它会不会用“工具”（如果有工具的话）
如果是计算器：

text
帮我算一下 25 乘以 4 等于多少？
如果是时间工具：

text
现在几点了？
如果是读文件工具（如果你在 project1 里加了）：

text
帮我读一下 daily_log.txt 写份周报。
