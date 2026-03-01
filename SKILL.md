---
name: codeflicker
description: CodeFlicker CLI 编程助手。用于安装、配置 CodeFlicker 并使用它来编写代码。当用户提到 flickcli、codeflicker、安装 codeflicker、使用 codeflicker 写代码时使用此技能。
---

# CodeFlicker CLI 技能

CodeFlicker 是快手开发的 AI 编程助手命令行工具，功能类似 Claude Code 或 Codex CLI。

## 使用场景

- 用户想安装 CodeFlicker CLI
- 用户想配置 CodeFlicker（模型、审批模式等）
- 用户想用 CodeFlicker 写代码
- 用户想和 CodeFlicker 对话

## 安装

### 方式一：npm（需要快手内部源）

```bash
npm install -g @ks-codeflicker/cli
```

### 方式二：检查是否已安装

```bash
which flickcli
flickcli --version
```

## 配置

### 查看配置

```bash
flickcli config list          # 当前项目配置
flickcli config list -g       # 全局配置
flickcli config get model     # 查看具体配置
```

### 设置配置（全局）

```bash
# 主模型
flickcli config set -g model glm-5

# 轻量模型（简单任务用，速度快）
flickcli config set -g smallModel claude-haiku-4.5

# 规划模型（复杂任务规划）
flickcli config set -g planModel claude-4.5-sonnet

# 视觉模型（图片分析）
flickcli config set -g visionModel claude-4.5-sonnet

# 审批模式
flickcli config set -g approvalMode yolo    # 自动执行，无需确认
flickcli config set -g approvalMode autoEdit # 自动编辑
flickcli config set -g approvalMode default  # 默认确认
```

### 可用模型（万擎 provider）

| 用途 | 模型 ID |
|------|---------|
| 主模型 | glm-5 |
| 轻量模型 | glm-4.7, claude-haiku-4.5 |
| 规划模型 | claude-4.5-sonnet |
| 视觉模型 | claude-haiku-4.5, claude-4.5-sonnet |

## 使用方式

### 交互模式

```bash
flickcli "帮我写一个 Hello World"
```

### 安静模式（非交互）

```bash
flickcli -q "写一个函数实现斐波那契数列"
```

### 继续上次对话

```bash
flickcli -q -c "再添加单元测试"
```

### 指定模型

```bash
flickcli -m glm-5 "任务描述"
flickcli --small-model claude-haiku-4.5 "简单任务"
```

### 指定工作目录

```bash
flickcli --cwd /path/to/project "任务描述"
```

## 常用命令速查

| 命令 | 功能 |
|------|------|
| `flickcli "任务"` | 交互模式执行任务 |
| `flickcli -q "任务"` | 安静模式（非交互） |
| `flickcli -q -c "继续"` | 继续上次对话 |
| `flickcli -q -r <session-id> "任务"` | 恢复指定会话 |
| `flickcli config set -g model glm-5` | 设置默认模型 |
| `flickcli config set -g approvalMode yolo` | 设置自动执行模式 |
| `flickcli --help` | 查看帮助 |

## 环境变量

| 变量 | 说明 |
|------|------|
| `WANQING_API_KEY` | 万擎 provider 的 API key |

## 注意事项

1. 安装可能需要快手内部 npm 源
2. 首次使用需要登录：`flickcli /login`
3. yolo 模式下会自动执行所有操作，请谨慎使用
4. 安静模式 (`-q`) 适合自动化脚本调用