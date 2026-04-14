# AI智能伴侣

一个基于 Streamlit 和 DeepSeek AI 的智能对话伴侣应用，支持会话管理、个性化定制和历史记录保存。

## ✨ 功能特性

- 🤖 **智能对话**：集成 DeepSeek AI 大模型，提供自然流畅的对话体验
- 💬 **流式响应**：实时显示 AI 回复，无需等待完整生成
- 📝 **会话管理**：支持创建、加载、删除多个会话
- 💾 **数据持久化**：使用 SQLite 数据库存储会话历史
- 🎭 **个性化定制**：可自定义 AI 伴侣的昵称和性格
- 🕐 **历史记录**：自动保存所有对话，按时间排序展示
- 🎨 **友好界面**：基于 Streamlit 的现代化 Web 界面

## 🛠️ 技术栈

- **前端框架**：Streamlit
- **AI 模型**：DeepSeek Chat (deepseek-chat)
- **数据存储**：SQLite
- **API 客户端**：OpenAI Python SDK
- **编程语言**：Python 3.8+

## 📦 安装依赖

```bash
pip install streamlit openai
```

## ⚙️ 环境配置

1. 获取 DeepSeek API Key
   - 访问 [DeepSeek 官网](https://platform.deepseek.com/) 注册账号
   - 在控制台生成 API Key

2. 设置环境变量
   ```bash
   # Windows PowerShell
   $env:DEEPSEEK_API_KEY="your-api-key-here"
   
   # Linux/Mac
   export DEEPSEEK_API_KEY="your-api-key-here"
   ```

   或者在项目根目录创建 `.env` 文件（需要安装 `python-dotenv`）：
   ```
   DEEPSEEK_API_KEY=your-api-key-here
   ```

## 🚀 运行应用

```bash
cd ai
streamlit run AI智能伴侣.py
```

应用将在浏览器中自动打开，默认地址为 `http://localhost:8501`

## 📖 使用说明

### 1. 开始对话
- 在底部输入框输入你的问题或消息
- 点击发送或按 Enter 键
- AI 会实时显示回复内容

### 2. 个性化设置
在左侧边栏的"伴侣信息"区域：
- **伴侣昵称**：设置 AI 的名字（默认：小美）
- **伴侣性格**：描述 AI 的性格特点（默认：成熟、独立、自信）

### 3. 会话管理

#### 新建会话
- 点击侧边栏顶部的"✏️ 新建会话"按钮
- 当前会话会自动保存
- 创建一个新的空白会话

#### 加载历史会话
- 在"历史会话"列表中点击任意会话名称
- 📜 图标表示加载该会话
- 当前会话会以蓝色高亮显示

#### 删除会话
- 点击会话名称旁边的 🗑️ 图标
- 确认删除后，该会话将从数据库中移除

### 4. 数据存储

所有会话数据保存在 `sessions.db` SQLite 数据库文件中：

**数据库表结构**：
```sql
CREATE TABLE sessions (
    session_name TEXT PRIMARY KEY,  -- 会话名称（时间戳格式）
    nick_name TEXT NOT NULL,        -- AI 伴侣昵称
    nature TEXT NOT NULL,           -- AI 伴侣性格描述
    messages TEXT NOT NULL,         -- 聊天消息（JSON 格式）
    created_at TIMESTAMP            -- 创建时间
)
```

## 📁 项目结构

```
ai/
├── AI智能伴侣.py          # 主应用程序
├── resources/              # 资源文件目录
│   ├── logo.png           # 应用 Logo
│   ├── img.png            # 其他图片资源
│   ├── user.json          # 用户配置（可选）
│   ├── 视频.mp4           # 视频资源
│   └── 音频.mp3           # 音频资源
├── sessions.db            # SQLite 数据库（自动生成）
├── 01. deepseek调用测试.py    # DeepSeek API 测试脚本
├── 02. json模块入门.py       # JSON 模块学习示例
├── 02. streamlit入门.py      # Streamlit 学习示例
├── 03-06. ai_partner_*.py    # AI 伴侣迭代版本
└── sessions/               # 旧版 JSON 会话存储（已废弃）
```

## 🎯 系统提示词

应用内置了详细的系统提示词，定义了 AI 伴侣的行为准则：

- **角色定位**：专属 AI 伴侣，提供情绪支持和建议
- **核心行为**：主动关怀、记忆延续、平衡理性与感性
- **交互风格**：自然口语化、适当使用 emoji、开放式提问
- **特殊能力**：每日总结、提醒功能、小游戏、学习助手
- **禁忌限制**：不模拟专业人士、不提供危险内容

## 🔧 开发说明

### 核心函数

- `init_db()`: 初始化 SQLite 数据库和表结构
- `save_session()`: 保存当前会话到数据库
- `load_sessions()`: 加载所有会话列表
- `load_session(session_name)`: 加载指定会话
- `delete_session(session_name)`: 删除指定会话
- `generate_session_name()`: 生成会话名称（时间戳格式）

### 会话状态管理

使用 Streamlit 的 `session_state` 管理应用状态：
- `messages`: 当前会话的消息列表
- `nick_name`: AI 伴侣昵称
- `nature`: AI 伴侣性格描述
- `current_session`: 当前会话名称

## ⚠️ 注意事项

1. **API Key 安全**：不要将 API Key 提交到版本控制系统
2. **数据库备份**：定期备份 `sessions.db` 文件以防数据丢失
3. **网络要求**：需要稳定的网络连接以访问 DeepSeek API
4. **费用说明**：使用 DeepSeek API 可能产生费用，请关注使用情况

## 🐛 常见问题

### Q: 启动时提示找不到模块？
A: 确保已安装所有依赖：`pip install streamlit openai`

### Q: 对话没有响应？
A: 检查是否正确设置了 `DEEPSEEK_API_KEY` 环境变量

### Q: 如何查看历史会话？
A: 所有会话自动保存在 `sessions.db` 中，可在侧边栏查看

### Q: 可以导出会话记录吗？
A: 目前会话存储在 SQLite 数据库中，可使用数据库工具导出

## 📝 更新日志

### v2.0 (当前版本)
- ✅ 从 JSON 文件存储迁移到 SQLite 数据库
- ✅ 优化会话加载性能
- ✅ 自动维护会话创建时间戳
- ✅ 改进数据一致性和安全性

### v1.0
- ✅ 基础对话功能
- ✅ 会话管理
- ✅ JSON 文件存储

## 📄 许可证

本项目仅供学习和研究使用。

## 🤝 贡献

欢迎提出建议和反馈！

---

**享受与 AI 伴侣的智能对话体验！** 🎉
