---
title: Gateway 和 MCP 的区别
date: 2026-05-28
categories: AI基础
tags: [AI, Agent]
---
# Gateway 和 MCP 的区别

## 一句话

MCP 是协议标准，Gateway 是运行中的服务。它们不是同一个东西。

## 角色不同

| | MCP | Gateway |
|---|---|---|
| 是什么 | 协议标准 | 一个运行中的服务进程 |
| 负责 | 定义"工具该怎么描述、该怎么调用" | 定义"消息从哪来、到哪去、谁处理" |
| 类比 | USB-C 接口规范 | 路由器 |

## 打个比方

```
你说话 → 音箱听到 → 路由器分发指令 → 调不同的智能家居设备

你的声音         = 各种消息渠道（飞书、WhatsApp...）
路由器/分发      = Gateway（决定"这条消息谁处理"）
USB-C 接口      = MCP（决定"设备之间怎么通信"）
智能家居设备     = 各种工具（查天气、发邮件、读数据库...）
```

## 在 OpenClaw 中的关系

```
飞书用户发消息
     ↓
Gateway 收到 → 判断"这是飞书渠道来的，路由到 agent A"
     ↓
agent A 思考 → 决定调工具"查天气"
     ↓
通过 MCP 协议 → 调天气 MCP Server → 返回结果
     ↓
agent A 生成回复 → Gateway 把回复送回飞书
```

## Gateway 为什么比 MCP 复杂

MCP 只管工具格式。Gateway 还要管：

- 多渠道适配（飞书、WhatsApp、Telegram 格式都不同）
- 会话状态管理（谁在跟哪个 agent 聊天）
- 可靠性和去重
- 安全和权限控制
