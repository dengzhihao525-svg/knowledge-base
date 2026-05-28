---
title: Agent 是什么
date: 2026-05-28
categories: AI基础
tags: [AI, Agent]
---
# Agent 是什么

## 一句话

Agent = LLM（大脑）+ 工具（手）+ 循环（决策链）。

## 核心循环

```
用户说一句话 → LLM 思考 → 决定要用什么工具 → 执行工具 → 拿到结果 → LLM 再思考 → 下一步...
```

循环一直跑，直到 LLM 觉得"任务完成了，可以回复用户"。

## 三个关键部件

**LLM（大脑）**
就是大模型本身。它负责理解你的意图、拆解任务、决定下一步做什么。

**工具（手）**
就是给 LLM 能调用的函数——搜文件、读网页、执行命令等。每个工具要告诉 LLM：我叫什么、我能干嘛、参数是什么。

**循环控制（决策链）**
LLM 每一轮输出要么是"调工具"，要么是"回复用户"。调完工具后把结果塞回对话里，让 LLM 决定下一步。

## 简化版代码

```python
messages = [{"role": "user", "content": "帮我建个项目"}]

while True:
    response = llm.chat(messages, tools=tools)  # LLM 思考
    
    if response.has_tool_call:
        result = execute(response.tool_name, response.params)  # 执行工具
        messages.append({"role": "tool", "content": result})   # 结果塞回去
    else:
        print(response.text)  # 任务完成，回复用户
        break
```

## 例子：查天气 Agent

1. 用户："北京今天天气怎么样"
2. LLM 思考："我需要调用 get_weather 工具，参数 city='北京'"
3. 工具返回：{"temp": 27, "weather": "晴"}
4. LLM 思考："拿到结果了，回复用户：北京今天晴，27度"
5. 结束

## 与你用的 Claude Code 的关系

Claude Code 本身就是一个 Agent——它能读文件、写代码、执行命令，都是 LLM + 工具 + 循环这套逻辑运作的。
