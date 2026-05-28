---
title: Token 怎么消耗
date: 2026-05-28
categories: AI基础
tags: [AI, Agent]
---
# Token 怎么消耗

## 一句话

每次调 LLM API，按输入和输出的 token 数量计费。

## Token 是什么

Token 是 LLM 处理文本的最小单位。粗略算：1 个中文字 ≈ 1-2 个 token，1 个英文单词 ≈ 1-3 个 token。

## Agent 的 Token 消耗

Agent 每轮思考都要调一次 API，上下文中包含系统提示词、工具定义、对话历史等：

```
你: "帮我查一下北京天气"

第1轮 → LLM 思考 → "我该调用 get_weather"
        → ~200 input tokens + ~100 output tokens

工具返回 → "北京晴，27度"

第2轮 → LLM 思考 → "拿到结果了，总结回复用户"
        → ~300 input tokens + ~150 output tokens

总消耗: ~750 tokens
```

## 省钱技巧

- **用小模型** — Haiku 比 Opus 便宜几十倍
- **限制循环轮次** — 设上限防止无限循环烧钱
- **精简上下文** — 对话历史越短越省钱
- **Prompt Caching** — 缓存重复的 system prompt，省 90% input 费

## API Key 怎么连接

```
你的程序 → 读 .env 文件拿 key → SDK 带上 key 发 HTTPS 请求 
→ Anthropic 服务器验证 → 跑模型 → 扣费 → 返回结果
```
