XitingBot - 自动回复机器人
<p align="center"> <img src="https://img.shields.io/badge/python-3.7+-blue.svg"> <img src="https://img.shields.io/badge/license-MIT-green.svg"> <img src="https://img.shields.io/badge/API-DeepSeek-orange.svg"> <img src="https://img.shields.io/badge/微信-自动回复-brightgreen.svg"> </p><p align="center"> 🤖 一个拥有"沈溪亭"人设的智能微信机器人，基于DeepSeek API实现自然对话 </p>
📋 目录
功能特点

实现方式

扩展方向

可修改设置

快速开始

配置文件说明

注意事项

✨ 功能特点
1. 🤖 智能对话
DeepSeek API集成：使用先进的DeepSeek大语言模型

人设定制：内置"沈溪亭"人设

上下文理解：保持10条最近对话的临时记忆

时间感知：根据时间段自动调整回复风格

2. 🧠 记忆系统
核心记忆：长期保存用户的重要信息（姓名、生日、喜好等）

临时记忆：最近10条对话的短期记忆

自动学习：从对话中提取重要信息并保存

记忆持久化：所有记忆自动保存到JSON文件

3. 💬 主动聊天
定时问候：每隔60-120分钟自动发送问候消息

智能休眠：23:00-8:00自动进入免打扰模式

手动触发：按A键随时发送主动消息

个性化消息：根据时间、场景生成不同内容

4. 🔍 智能检测
重复过滤：自动识别并跳过重复消息（相似度>80%）

自我识别：不会回复自己发送的消息

精准获取：自动捕获微信最新消息

防刷屏：合理的时间间隔控制

5. 🎯 操作便捷
一键校准：简单的坐标校准工具

热键控制：ESC暂停/继续，H查看状态，C清空记忆

状态显示：实时显示运行状态、记忆数量、下次主动消息时间

自动保存：所有配置和记忆自动保存

🔧 实现方式
技术架构
text
┌─────────────────┐
│    微信客户端    │
└────────┬────────┘
         ▼
┌─────────────────┐
│  pyautogui操作  │  ← 模拟鼠标点击、键盘输入
│  pyperclip剪贴板│  ← 复制粘贴消息
└────────┬────────┘
         ▼
┌─────────────────┐
│  消息处理引擎    │  ← 重复检测、自我识别、记忆管理
└────────┬────────┘
         ▼
┌─────────────────┐
│  DeepSeek API   │  ← 智能对话生成
└─────────────────┘
核心模块
模块	功能	技术实现
消息捕获	获取最qq信消息	三击消息区域 + Ctrl+C复制
消息发送	自动回复消息	定位输入框 + Ctrl+V粘贴 + 回车
对话生成	智能回复	DeepSeek API + 人设提示词
记忆管理	信息持久化	JSON文件存储 + 自动提取
热键控制	实时控制程序	keyboard库监听快捷键
状态显示	运行状态监控	控制台实时输出
关键代码示例
python
# 消息捕获
def get_last_message(coords):
    pyautogui.click(x, y)  # 三击选中
    pyautogui.hotkey('ctrl', 'c')  # 复制
    return pyperclip.paste()  # 获取内容

# API调用
def call_deepseek_api(user_msg):
    messages = [
        {"role": "system", "content": personality_prompt},
        {"role": "user", "content": user_msg}
    ]
    response = requests.post(API_URL, json=payload)
    return response.json()['choices'][0]['message']['content']
🚀 扩展方向
1. 📱 多平台支持
text
┌─────────────┐
│   微信      │ ← 可支持
├─────────────┤
│   QQ        │ ← 当前支持
├─────────────┤
│   钉钉      │ ← 可支持
├─────────────┤
│   Telegram  │ ← 可支持
├─────────────┤
│   Discord   │ ← 可支持
└─────────────┘
2. 🧠 记忆系统升级
向量数据库：使用Chroma/FAISS实现长期记忆检索

情感分析：识别用户情绪并调整回复语气

兴趣图谱：构建用户兴趣关系网络

多模态记忆：支持图片、语音的记忆

3. 🤖 功能增强
python
# 计划添加的功能
扩展功能清单：
✅ 基础对话
✅ 主动问候
⬜ 定时任务（提醒、日报）
⬜ 多账号支持
⬜ 插件系统
⬜ Web管理界面
⬜ 语音回复
⬜ 图片识别
⬜ 联网搜索
4. 📊 数据分析
对话统计（次数、时长、主题）

情感趋势分析

用户画像构建

回复效果评估

5. 🔌 API集成扩展
yaml
潜在集成服务:
  天气API: "根据天气调整问候语"
  新闻API: "分享最新资讯"
  日历API: "提醒重要日期"
  音乐API: "推荐歌曲"
  翻译API: "多语言支持"
⚙️ 可修改设置
配置文件 config/settings.py
python
# ========== API配置 ==========
API_KEY = "sk-xxxxxxxxxxxx"  # 你的DeepSeek API Key
API_URL = "https://api.deepseek.com/v1/chat/completions"
MODEL = "deepseek-chat"  # 可改为其他模型
POLL_INTERVAL = 3  # 轮询间隔（秒）

# ========== 人设配置 ==========
PERSONALITY_PROMPT_FILE = "personality_prompt.txt"  # 人设文件路径
# 可修改人设文件内容完全改变AI性格

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
SLEEP_END_HOUR = 8     # 睡眠结束时间

# ========== 调试模式 ==========
DEBUG_MODE = True  # 显示详细日志
人设文件 personality_prompt.txt
你可以完全修改这个文件来改变AI的性格：

txt
【示例：知性姐姐人设】
你是一个知性温柔的姐姐，28岁...
【示例：搞笑朋友人设】
你是一个幽默风趣的好朋友，喜欢讲段子...
【示例：专业助手人设】
你是一个专业的个人助理，做事严谨认真...
主动消息模板 active_messages.json
自定义自动问候的内容：

json
[
    "今天过得怎么样呀？",
    "想听个笑话吗？",
    "分享个有趣的事..."
]
坐标配置文件 wechat_auto_reply_config.json
json
{
    "last_msg_x": 100,  // 最后消息X坐标
    "last_msg_y": 200,  // 最后消息Y坐标
    "input_box_x": 300, // 输入框X坐标
    "input_box_y": 400  // 输入框Y坐标
}
🚀 快速开始
安装步骤
克隆仓库

bash
git clone https://github.com/你的用户名/XitingBot.git
cd XitingBot
安装依赖

bash
# Windows
install.bat

# 或手动安装
pip install -r requirements.txt
配置API密钥

在 config/settings.py 中填入你的DeepSeek API Key

获取地址：https://platform.deepseek.com/

运行程序

bash
python main.py
校准坐标

按提示将鼠标移到微信窗口

分别点击最后消息位置和输入框位置

按回车确认

使用快捷键
快捷键	功能
H	显示状态
C	清空临时记忆
ESC	暂停/继续
A	手动发送主动消息
Ctrl+C	退出程序
📁 配置文件说明
文件结构
text
XitingBot/
├── main.py                 # 主程序
├── config/
│   └── settings.py        # 配置文件
├── core/
│   ├── personality.py     # 人设管理
│   ├── memory.py          # 记忆管理
│   └── message_manager.py # 消息管理
├── api/
│   └── deepseek_client.py # API客户端
├── utils/
│   ├── helpers.py         # 工具函数
│   ├── coordinate.py      # 坐标管理
│   └── message_utils.py   # 消息工具
├── hotkeys/
│   └── manager.py         # 热键管理
├── ui/
│   └── status_display.py  # 状态显示
├── install.bat            # 安装脚本
├── start.bat             # 启动脚本
├── requirements.txt      # 依赖列表
└── README.md             # 本文档
自动生成的文件
文件	用途	是否可修改
personality_prompt.txt	AI人设提示词	✅ 可修改
core_memory.json	核心记忆存储	⚠️ 自动生成
chat_history.json	临时记忆存储	⚠️ 自动生成
active_messages.json	主动消息模板	✅ 可修改
wechat_auto_reply_config.json	坐标配置	⚠️ 自动生成
⚠️ 注意事项
使用前须知
该项目在不同程序如wechat或QQ中应用大概率需要修改点击方式代码默认点击方式适配QQ

API费用

DeepSeek API 是付费服务

请关注API调用次数和费用

使用规范

请遵守用户协议

不要用于营销、骚扰等违规用途

建议使用小号测试

坐标校准

建议将聊天软件最大化进行校准和使用

确保窗口未被最小化或遮挡

程序限制

仅支持Windows系统

需要保持微信窗口在前台

不能处理图片和语音消息

常见问题
Q: 程序无法获取消息？
A: 重新校准坐标，确保点击位置准确

Q: API调用失败？
A: 检查API Key是否正确，网络是否通畅

Q: 如何完全重置？
A: 删除生成的JSON文件即可重置所有配置

📄 许可证
MIT License © 2024 沈溪亭

🙏 致谢
DeepSeek - 提供强大的AI API

PyAutoGUI - 自动化操作库

所有贡献者和用户

<p align="center"> 如果这个项目对你有帮助，请给个 ⭐️ </p><p align="center"> <a href="https://github.com/你的用户名/XitingBot/issues">报告问题</a> · <a href="https://github.com/你的用户名/XitingBot/pulls">提交PR</a> · <a href="#-目录">返回顶部</a> </p> ```
