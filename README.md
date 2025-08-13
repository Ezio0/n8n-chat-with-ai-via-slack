# Gemini Slack Bot

这是一个基于n8n平台构建的Slack机器人工作流，它使用Google Gemini AI模型来回答用户在Slack中提出的问题。

![alt text](<Preview_workflow.png>)

## 功能特点

- 监听Slack中的应用提及（@gemini）
- 使用Google Gemini 2.5 Pro模型进行对话
- 支持实时信息查询（通过Tavily工具）
- 在特定Slack频道中回复用户消息
- 支持markdown格式在Slack中展示
- **支持会话记忆功能**：保留用户对话上下文
- **支持新会话命令**：使用特定命令开始新的对话

## 工作流结构

### 触发器
- **Slack Trigger**: 监听Slack中的应用提及事件

### 核心组件
1. **Session Manager**: 处理新会话命令和用户输入
2. **AI Agent**: 处理用户问题的核心AI代理
3. **Google Gemini Chat Model**: 使用Gemini 2.5 Pro模型进行对话
4. **Chat Memory Manager**: 管理对话内存
5. **Simple Memory**: 存储对话历史
6. **MCP Client Tools**: 提供实时搜索功能（Tavily工具）

### 输出
- **Send a message**: 将AI回复发送回Slack频道

## 工作原理

1. 当用户在Slack中@机器人时，触发器会捕获消息
2. Session Manager检查是否是新会话命令
3. 如果是新会话命令，则清除用户的对话历史
4. AI代理接收用户消息，并根据核心原则进行处理：
   - 优先使用内部知识库回答问题
   - 只有在需要实时信息时才调用外部工具
5. 如果需要实时信息，AI会调用Tavily搜索工具
6. 最终回复通过Slack发送回用户

## 使用说明

1. 确保已配置Slack API凭证
2. 确保已配置Google Gemini API凭证
3. 确保已配置MCP Client Tavily凭证
4. 在Slack中@机器人并提问

### 会话命令

- **开始新会话**：发送 `/新对话` 命令来开始新的对话
- **继续对话**：直接提问即可继续之前的对话

## 配置要求

- Slack API凭证
- Google Gemini API密钥
- Tavily API密钥（通过MCP Client配置）