---
title: MCP 是什么
date: 2026-05-28
categories: AI基础
tags: [AI, Agent]
---
# MCP 是什么

## 一句话

MCP = Model Context Protocol（模型上下文协议），是工具调用的 USB-C 标准。

## 为什么需要 MCP

**没有 MCP**：每个工具接入方式都不一样，你得为每个工具单独写对接代码。

**有了 MCP**：所有工具都用同一套协议，LLM 通过 MCP 统一调用：

```
LLM ──MCP──→ GitHub MCP Server ──→ 操作 GitHub
LLM ──MCP──→ 飞书 MCP Server  ──→ 操作飞书
LLM ──MCP──→ 数据库 MCP Server ──→ 操作数据库
```

## 本质

MCP Server 就是一个小程序，定义了一套 LLM 能懂的"我有哪些功能、参数是什么"，LLM 发请求过来，它执行完返回结果。

## MCP 和 Gateway 的区别

| | MCP | Gateway |
|---|---|---|
| 是什么 | 协议标准 | 运行中的服务进程 |
| 管什么 | 工具调用格式 | 消息路由和分发 |
| 类比 | USB-C 接口规范 | 路由器 |

它们是上下层关系：Gateway 在上层管"谁的请求、交给谁、回给谁"，MCP 在下层管"工具怎么调、参数怎么传、结果怎么返回"。
