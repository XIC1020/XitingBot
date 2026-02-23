XitingBot - 自动回复机器人
<p align="center"> <img src="https://img.shields.io/badge/python-3.7+-blue.svg"> <img src="https://img.shields.io/badge/license-MIT-green.svg"> <img src="https://img.shields.io/badge/API-DeepSeek-orange.svg"> </p><p align="center"> 默认状态下为基于DeepSeek API的QQ机器人 </p>
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
