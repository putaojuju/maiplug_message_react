# maiplug_message_react

麦麦插件 | 让麦麦根据聊天内容智能匹配并贴附表情，提升群聊互动趣味性

## 📌 版本更新
- 版本号：`1.0.1`
- 更新内容：修复插件运行时出现的 `'int' object has no attribute 'strip'` 报错问题。

## 🎯 功能亮点
- 智能表情匹配：依托 LLM 能力，麦麦可根据消息内容自动选择贴合语境的表情
- 轻量化配置：仅需 3 项核心参数配置，快速完成部署

## 📸 效果展示
<img width="832" height="427" alt="插件使用效果" src="https://github.com/user-attachments/assets/e0a68cd3-718b-464b-b9e8-e7c1926421c3" />

## 📋 前置条件
1. 麦麦机器人已完成部署并正常运行，可响应群聊消息
2. Napcat 组件已安装且处于启动状态
3. 麦麦配置文件 `model_config.toml` 中，`model_task_config.tool_use` 项已配置完成，确保模型具备工具调用能力

## 🚀 安装与配置步骤
### 步骤1：部署插件
将插件文件放入麦麦主程序的 `plugins` 目录（通常位于麦麦安装根目录下）

### 步骤2：生成配置文件
重启麦麦主程序，插件会自动在 `plugins/maiplug_message_react` 目录下生成 `config.toml` 配置文件，如果没有请查看主程序加载插件的日志。

### 步骤3：配置 Napcat HTTP 服务
1. 打开 Napcat WebUI 控制台（默认访问地址：`http://{你的麦麦IP}:3001`）
2. 进入**网络配置**菜单，点击**添加 HTTP 服务器**
3. 按以下参数配置并保存：
   - Host：填写 `127.0.0.1`
   - Port：自定义未被占用的端口号（如 `3001`）
   - 其余选项保持默认值

### 步骤4：完善插件配置文件
使用文本编辑器打开自动生成的 `config.toml`，按下方说明补充配置项：

```toml
# maiplug_message_react - 自动生成的配置文件
# 通过 Napcat API 赋予麦麦对消息贴表情的能力

# 插件基本信息（无需修改）
[plugin]
name = "maiplug_message_react"
version = "1.0.1"  # 对应版本更新后的版本号
enabled = true     # true=启用插件，false=禁用插件

[napcat]
# Napcat服务地址：本地部署填 127.0.0.1；Docker部署填 napcat
host = "127.0.0.1"

# Napcat服务端口：填写步骤3中设置的自定义端口
port = "填写步骤3中设置的自定义端口"

# Napcat服务认证Token：从Napcat控制台获取
token = "步骤3 的Napcat访问Token"
   # maiplug_message_react - 自动生成的配置文件
   # 通过 Napcat API 赋予麦麦对消息贴表情的能力

   # 插件基本信息（无需修改）
   [plugin]
   name = "maiplug_message_react"
   version = "1.0.1"  # 对应版本更新后的版本号
   enabled = true     # true=启用插件，false=禁用插件

   [napcat]
   # Napcat服务地址：本地部署填 127.0.0.1；Docker部署填 napcat
   host = "127.0.0.1"

   # Napcat服务端口：填写步骤3中设置的自定义端口
   port = "填写步骤3中设置的自定义端口"

   # Napcat服务认证Token：从Napcat控制台获取
   token = "步骤3 的Napcat访问Token"
```
#### 🔍 如何获取 Napcat Token
1. 回到 Napcat WebUI 控制台
2. 进入**设置 → 安全设置**（或**Token管理**）页面
3. 复制系统生成的**访问Token**，粘贴到配置文件的 `token` 项中（注意保留引号）

### 步骤5：启动插件
保存配置文件后，再次重启麦麦主程序，插件即可正式生效

## ❓ 常见问题排查
| 问题现象 | 解决方法 |
|----------|----------|
| 插件启用失败，提示配置错误 | 检查 `config.toml` 中 `host`/`port`/`token` 是否填写正确，确认 Napcat HTTP 服务处于运行状态 |
| 麦麦可回复消息，但不贴表情 | 更换具备工具调用能力的模型（推荐火山引擎 `doubao-seed-1-6-25061`），并校验 `model_config.toml` 中 `tool_use` 配置 |
| 提示“Token无效” | 重新从 Napcat 控制台获取 Token，确保配置文件中无多余空格或特殊符号 |

## 💡 温馨提示
- 配置文件仅需修改 `[napcat]` 模块下的 3 项参数，其余内容请勿改动
- Docker 部署场景下，需确保麦麦容器与 Napcat 容器处于同一网络环境
- 若插件运行异常，可查看麦麦日志文件定位具体问题，将报错内容复制发送给大模型分析可以解决99%的问题