maiplug_message_react
麦麦插件 | 让麦麦根据聊天内容智能匹配并贴附表情，提升群聊互动趣味性
📌 版本更新
版本号：1.0.1
更新内容：修复插件运行时出现的 'int' object has no attribute'strip' 报错问题，优化插件稳定性，提升运行流畅度
🎯 功能亮点
智能表情匹配：依托 LLM 能力，麦麦可根据消息内容自动选择贴合语境的表情
轻量化配置：仅需 3 项核心参数配置，快速完成部署
环境兼容友好：完美适配麦麦官方 Docker 部署环境与本地部署环境
📸 效果展示
PixPin_2025-09-01_22-10-20
https://github.com/user-attachments/assets/e0a68cd3-718b-464b-b9e8-e7c1926421c3
📋 前置条件
麦麦机器人已完成部署并正常运行，可响应群聊消息
Napcat 组件已安装且处于启动状态
麦麦配置文件 model_config.toml 中，model_task_config.tool_use 项已配置完成，确保模型具备工具调用能力
🚀 安装与配置步骤
步骤 1：部署插件
将插件文件放入麦麦机器人的 plugins 目录（通常位于麦麦安装根目录下）
步骤 2：生成配置文件
重启麦麦机器人，插件会自动在 plugins/maiplug_message_react 目录下生成 config.toml 配置文件
步骤 3：配置 Napcat HTTP 服务
打开 Napcat WebUI 控制台（默认访问地址：http://{你的麦麦 IP}:3001）
进入 网络配置 菜单，点击 添加 HTTP 服务器
按以下参数配置并保存：
Host：填写 0.0.0.0（putaojuju:一键包填写127.0.0.1）
Port：自定义未被占用的端口号（如 3000）
其余选项保持默认值
步骤 4：完善插件配置文件
使用文本编辑器打开自动生成的 config.toml，按下方说明补充配置项：
maiplug_message_react - 自动生成的配置文件
通过 Napcat API 赋予麦麦对消息贴表情的能力
插件基本信息（无需修改）
[plugin]
name = "maiplug_message_react"
version = "1.0.1" # 对应版本更新后的版本号
enabled = true # true = 启用插件，false = 禁用插件
[napcat]
Napcat 服务地址：
host = "本地部署填 127.0.0.1；Docker 部署填 napcat"
Napcat 服务端口：填写步骤 3 中设置的自定义端口
port = "填写步骤 3 中设置的自定义端口"
Napcat 服务认证 Token：从 Napcat 控制台获取
token = "步骤3时的 Napcat 访问 Token"
步骤 5：启动插件
保存配置文件后，再次重启麦麦机器人，插件即可正式生效
📢 使用方法
在麦麦所在的群聊中，@麦麦 并发送任意消息（例如：@麦麦 今天的天气真不错），麦麦会自动识别消息内容并贴附对应的表情
❓ 常见问题排查
问题现象	解决方法
插件启用失败，提示配置错误	检查 config.toml 中 host/port/token 是否填写正确，确认 Napcat HTTP 服务处于运行状态
麦麦可回复消息，但不贴表情	更换具备工具调用能力的模型（推荐火山引擎 doubao-seed-1-6-25061），并校验 model_config.toml 中 tool_use 配置
提示 “Token 无效”	重新从 Napcat 控制台获取 Token，确保配置文件中无多余空格或特殊符号
💡 温馨提示
配置文件仅需修改 [napcat] 模块下的 3 项参数，其余内容请勿改动
Docker 部署场景下，需确保麦麦容器与 Napcat 容器处于同一网络环境
若插件运行异常，可查看麦麦日志文件定位具体问题