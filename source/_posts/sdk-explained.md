---
title: SDK 是什么
date: 2026-05-28
categories: AI基础
tags: [AI, Agent]
---
# SDK 是什么

## 一句话

SDK = Software Development Kit（软件开发工具包），就是官方帮你写好的轮子。

## 为什么需要 SDK

**没有 SDK** 时，你得自己发 HTTP 请求、管理连接、处理重试、处理错误：

```python
import requests
import json

response = requests.post(
    "https://api.anthropic.com/v1/messages",
    headers={"x-api-key": "你的key", "anthropic-version": "..."},
    json={"model": "claude-opus-4-7", "messages": [...]}
)
```

**有了 SDK**，三行搞定：

```python
import anthropic

client = anthropic.Anthropic(api_key="你的key")
response = client.messages.create(
    model="claude-opus-4-7",
    messages=[{"role": "user", "content": "你好"}]
)
```

SDK 帮你处理了连接池、重试、流式输出、错误处理这些脏活累活，你只需要关心业务逻辑。

## 常见 SDK

| SDK | 用途 |
|-----|------|
| `pip install anthropic` | 调 Claude API |
| `npm install openai` | 调 OpenAI API |
| `pip install boto3` | 操作 AWS 资源 |
| 飞书 SDK | 调飞书 API |
