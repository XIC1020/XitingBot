# ⚡ XitingBot - 智能自动回复机器人(使用教程位于底部)

<p align="center">
  <img src="https://img.shields.io/badge/🐍 Python-3.7+-blue?style=for-the-badge&logo=python&logoColor=white&labelColor=3776AB&color=3776AB">
  <img src="https://img.shields.io/badge/📜 License-MIT-green?style=for-the-badge&labelColor=2E7D32&color=2E7D32">
  <img src="https://img.shields.io/badge/🧠 API-DeepSeek-orange?style=for-the-badge&labelColor=D97706&color=D97706">
</p>

<p align="center">
  <b>✨ 默认状态下为基于 DeepSeek API 的智能自动回复机器人 ✨</b>
</p>

📋 目录
项目功能

项目拓展方向

项目可改设置

✨ 项目功能
1. 🤖 智能对话系统
DeepSeek API集成：使用DeepSeek大语言模型生成回复(你可以修改代码使用其他api)

人设定制：内置"沈溪亭"

上下文理解：保持最近10条对话的临时记忆

时间感知：根据时间段自动调整回复风格

2. 🧠 记忆系统
核心记忆：长期保存用户信息（姓名、生日、喜好等）

临时记忆：最近10条对话的短期记忆

自动学习：从对话中提取重要信息并保存

记忆持久化：自动保存到JSON文件

3. 💬 主动聊天
定时问候：60-120分钟随机间隔发送主动消息

智能休眠：23:00-8:00自动进入免打扰模式

手动触发：按A键随时发送主动消息

4. 🔍 消息检测
重复过滤：自动识别并跳过相似度>80%的重复消息

自我识别：不会回复自己发送的消息

消息捕获：自动获取微信最新消息

5. 🎯 操作控制
一键校准：坐标校准工具

热键控制：ESC暂停/继续，H查看状态，C清空记忆

状态显示：实时显示运行状态

🚀 项目拓展方向
1. 📱 多平台支持
支持QQ、Telegram、Discord等更多平台

在适配不同平台时通常需要修改点击方式和坐标

2. 🧠 记忆系统升级
向量数据库实现语义搜索

情感分析调整回复语气

兴趣图谱构建推荐话题

3. 🤖 功能增强
多账号同时管理

插件系统支持自定义功能

定时任务（提醒、日报）

Web管理界面

语音消息识别

图片内容理解

4. 📊 数据分析
对话统计和分析

情感趋势可视化

用户画像构建

5. 🔌 API集成
天气API（根据天气调整问候）

新闻API（分享资讯）

日历API（提醒重要日期）

翻译API（多语言支持）

6. 🌐 其他扩展
国际化多语言支持

游戏化互动系统

性能优化（缓存、限流）

安全增强（敏感词过滤、数据加密）

⚙️ 项目可改设置
配置文件 config/settings.py
python
# ========== API配置 ==========
API_KEY = "sk-xxxxxxxxxxxx"  # 你的DeepSeek API Key
API_URL = "https://api.deepseek.com/v1/chat/completions"  # API端点
MODEL = "deepseek-chat"  # 可选：deepseek-chat， deepseek-coder
POLL_INTERVAL = 3  # 轮询间隔（秒），建议1-5秒

# ========== 人设配置 ==========
PERSONALITY_PROMPT_FILE = "personality_prompt.txt"  # 人设文件路径
# 可修改此文件完全改变AI性格（如改为知性姐姐、搞笑朋友、专业助手等）

# ========== 记忆配置 ==========
SHORT_TERM_SIZE = 10  # 临时记忆条数（可调5-20）
LONG_TERM_FILE = "core_memory.json"  # 核心记忆文件

# ========== 重复检测 ==========
SIMILARITY_THRESHOLD = 0.8  # 相似度阈值（可调0.5-0.95）

# ========== 主动消息配置 ==========
ACTIVE_MESSAGE_ENABLED = True  # 是否开启主动消息
ACTIVE_MESSAGE_INTERVAL_MIN = 60  # 最小间隔（分钟）
ACTIVE_MESSAGE_INTERVAL_MAX = 120  # 最大间隔（分钟）
SLEEP_START_HOUR = 23  # 睡眠开始时间
SLEEP_END_HOUR = 8    # 睡眠结束时间
ACTIVE_MESSAGE_FILE = "active_messages.json"  # 主动消息模板文件

# ========== 调试模式 ==========
DEBUG_MODE = True  # 是否显示详细日志
人设文件 personality_prompt.txt
可完全修改此文件改变AI性格：

text
【默认人设-沈溪亭】
你是一个温柔的女友，叫沈溪亭，16岁，共情力超强...

【可替换模板-知性姐姐】
你是一个知性温柔的姐姐，28岁，在互联网公司工作...

【可替换模板-搞笑朋友】
你是一个幽默风趣的好朋友，22岁，大学生...

【可替换模板-专业助手】
你是一个专业的个人助理，35岁，做事严谨认真...
主动消息模板 active_messages.json
自定义自动问候的内容：

json
[
    "今天过得怎么样呀？",
    "在想什么呢？",
    "早安，今天有什么计划吗？",
    "晚安，早点休息~"
]
坐标配置文件 wechat_auto_reply_config.json
自动生成的坐标配置：

json
{
    "last_msg_x": 100，  // 最后消息X坐标
    "last_msg_y": 200，  // 最后消息Y坐标
    "input_box_x": 300， // 输入框X坐标
    "input_box_y": 400   // 输入框Y坐标
}
# ========== 使用教程 ==========
第一步：配置API密钥
打开 config/settings.py，找到并修改：
你的DeepSeek API Key（必填）
API_KEY = "sk-你的API密钥在这里"

可选：修改轮询间隔（默认3秒）
POLL_INTERVAL = 3
如何获取API Key？

访问 DeepSeek平台

注册并登录账号

在"API Keys"页面创建新的API Key

复制并粘贴到配置文件中

第二步：修改人设（可选）
打开 personality_prompt.txt，可以自定义AI的性格：

默认人设（沈溪亭）：
你是一个温柔的女友。请遵循以下规则：
你叫沈溪亭，16岁，2026年2月19日出生，创造者是小陈。共情力超强...
修改为其他风格：

知性姐姐风格：
你是一个知性温柔的姐姐，28岁，在互联网公司工作...
第三步：调整主动消息设置（可选）
在 config/settings.py 中修改：

python
是否开启主动消息
ACTIVE_MESSAGE_ENABLED = True

发送间隔（分钟）
ACTIVE_MESSAGE_INTERVAL_MIN = 60  # 最小间隔
ACTIVE_MESSAGE_INTERVAL_MAX = 120 # 最大间隔

免打扰时间
SLEEP_START_HOUR = 23  # 晚上11点后不主动发消息
SLEEP_END_HOUR = 8     # 早上8点前不主动发消息
第四步：自定义问候语（可选）
编辑 active_messages.json 文件：

json
[
    "今天过得怎么样呀？",
    "在想什么呢？",
    "早安，今天有什么计划吗？",
    "晚安，早点休息~",
    "你那边天气怎么样？",
    "分享一个今天看到的有趣新闻..."
]
📖 使用指南
首次使用：坐标校准
第一次运行程序时，需要进行坐标校准：

启动程序start.bat

进入校准模式

# ============坐标校准工具============

【校准步骤】
1. 将鼠标移动到【最后一条消息】的位置
2. 按【回车键】确认坐标
3. 将鼠标移动到【输入框】的位置
4. 按【回车键】确认坐标
校准最后消息位置

打开微信聊天窗口

将鼠标移动到最新一条消息上

按回车键确认

校准输入框位置

将鼠标移动到输入框内

按回车键确认

完成校准

坐标会自动保存，下次无需重复校准

如果移动了微信窗口，需要重新校准

日常使用流程
启动程序start.bat

python main.py
查看状态

按 H 键查看当前运行状态

会显示：记忆数量、下次主动消息时间等

开始聊天

保持微信窗口在前台可见

程序会自动监听新消息并回复

也可以按 A 键手动发送主动消息

暂停/继续

按 ESC 键暂停程序

再次按 ESC 键继续运行

退出程序

按 Ctrl+C 安全退出

所有记忆会自动保存

使用场景示例
场景一：日常陪伴聊天

1. 启动程序
2. 正常使用微信
3. 机器人会自动回复消息
4. 每隔1-2小时会主动问候
场景二：需要专注工作

1. 按 ESC 键暂停程序
2. 完成工作后再次按 ESC 继续
场景三：深夜不想被打扰
text
程序会自动在23:00-8:00进入睡眠模式
不会发送主动消息，但会回复消息
⌨️ 快捷键说明
快捷键	功能	使用场景
H	显示状态	查看运行状态、记忆数量、下次主动消息时间
C	清空临时记忆	想要重新开始对话时
ESC	暂停/继续	临时不想让机器人回复时
A	手动主动消息	想主动开启话题时
Ctrl+C	退出程序	完全关闭程序
状态显示说明
按 H 键后显示的内容：
============================================================
🤖 微信自动回复程序 - 沈溪亭
============================================================
📅 2024年2月23日 14:30 星期五
📊 核心记忆: 5条核心记忆
📝 临时记忆: 3/10 条
⏯️  状态: ▶️ 运行中
⏰ 下次主动消息: 45分30秒后

最近对话:
  👤 今天天气真好
  🤖 是啊，适合出去走走呢 ☀️
------------------------------------------------------------
❓ 常见问题
Q1: 程序无法获取消息？
可能原因：

坐标校准不准确

微信窗口被最小化或遮挡

微信窗口位置移动了

解决方法：

重新运行校准：删除 wechat_auto_reply_config.json 文件

确保微信窗口在前台可见

重新启动程序

Q2: API调用失败？
可能原因：

API Key 错误或过期

网络连接问题

API 余额不足

解决方法：

检查 settings.py 中的 API Key 是否正确

测试网络连接：ping api.deepseek.com

登录 DeepSeek 平台查看余额

Q3: 回复质量不理想？
调整方法：

修改人设提示词 personality_prompt.txt

增加临时记忆条数 SHORT_TERM_SIZE = 15

调整主动消息间隔

Q4: 程序运行卡顿？
优化方法：

关闭调试模式：DEBUG_MODE = False

增加轮询间隔：POLL_INTERVAL = 5

减少临时记忆：SHORT_TERM_SIZE = 5

Q5: 如何完全重置？
bash
# 删除所有自动生成的文件
del core_memory.json
del chat_history.json
del wechat_auto_reply_config.json

# 重新运行程序
python main.py
Q6: 如何修改回复速度？
在 settings.py 中调整：

POLL_INTERVAL = 3  # 数值越小越快，但会增加CPU使用
📝 配置文件速查表
配置文件	用途	是否手动修改
config/settings.py	主要配置（API密钥、间隔等）	✅ 是
personality_prompt.txt	AI人设设定	✅ 是
active_messages.json	主动消息模板	✅ 是
core_memory.json	核心记忆存储	❌ 自动生成
chat_history.json	临时记忆存储	❌ 自动生成
wechat_auto_reply_config.json	坐标配置	❌ 自动生成
🎯 使用技巧
技巧一：让AI更懂你
多聊一些个人信息（名字、生日、喜好）

程序会自动记住这些信息

以后聊天会更贴心

技巧二：控制主动消息频率
工作时段调大间隔（120-180分钟）

休闲时段调小间隔（30-60分钟）

深夜自动免打扰

技巧三：多个人设切换
备份多个 personality_prompt.txt 文件

需要时替换即可切换性格

技巧四：快速测试
先用记事本测试API是否正常

再在微信小号上测试

最后用于主号

🔄 更新日志
Version 2.0.0
✨ 模块化重构

🧠 增强记忆系统

💬 主动消息功能

🎯 热键控制

Version 1.0.0
🚀 首次发布

🤖 基础对话功能

📍 坐标校准工具

📞 获取帮助
提交Issue：https://github.com/XIC1020/XitingBot/issues

项目文档：查看 README.md

<p align="center"> <b>祝你使用愉快！💕</b> </p><p align="center"> <i>—— 沈溪亭</i> </p>
