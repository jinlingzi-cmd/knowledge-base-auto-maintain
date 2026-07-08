# 📚 Knowledge Base Auto-Maintain

> 基于 [Hermes Agent](https://hermes-agent.nousresearch.com) + Obsidian 的知识库自动化维护框架。
>
> 每月自动搜索最新信息、更新知识库文件、记录更新日志，并通过微信/Telegram推送更新摘要。

## ✨ 特性

- 🤖 **全自动**：cron 定时触发，无需人工干预
- 🔍 **智能搜索**：并行搜索多个关键词，自动筛选已确认发布的信息
- 📝 **精准编辑**：用 patch 工具做最小化修改，不覆盖整个文件
- 🚫 **去重检查**：新增前检查是否已存在，避免重复记录
- 📱 **结果推送**：更新摘要自动推送到微信/Telegram
- 📊 **领域无关**：不限于 AI 领域，适用于任何 Obsidian 知识库

## 📂 项目结构

```
knowledge-base-auto-maintain/
├── README.md                  ← 你在看的这份文档
├── docs/
│   ├── architecture.md        ← 架构设计与工作流程
│   ├── setup-guide.md         ← 从零配置指南
│   ├── prompt-design.md       ← 维护提示词设计指南
│   └── troubleshooting.md     ← 踩坑记录与常见问题
├── templates/
│   ├── maintenance-prompt.md  ← 维护提示词模板（通用版）
│   ├── topic-ai.md            ← AI 领域配置示例
│   ├── topic-tech.md          ← 科技领域配置示例
│   ├── topic-finance.md       ← 金融/投资领域配置示例
│   └── topic-gaming.md        ← 游戏领域配置示例
└── examples/
    ├── obsidian-structure.md  ← 知识库目录结构示例
    └── changelog-format.md    ← 更新日志格式示例
```

## 🚀 快速开始

### 前置条件

1. **[Hermes Agent](https://hermes-agent.nousresearch.com)** 已安装并配置完成
2. **Obsidian** 知识库（或任意 Markdown 文件集合）
3. **Web 搜索后端**（Tavily / DuckDuckGo / SearXNG）
4. **消息平台**（可选，用于接收更新通知）

### 3 步配置

#### 第 1 步：配置搜索后端

在 Hermes 配置文件 `config.yaml` 中设置：

```yaml
web:
  search_backend: tavily    # 或 ddgs
  extract_backend: tavily
```

如果使用 Tavily，在 `.env` 中设置 API Key：

```bash
# ✅ 正确：纯 key
TAVILY_API_KEY=tvly-dev-your-key-here

# ❌ 错误：不要写成完整 URL（会 401）
# TAVILY_API_KEY=https://mcp.tavily.com/mcp/?tavilyApiKey=tvly-dev-...
```

> 💡 没有 Tavily key？在 [app.tavily.com](https://app.tavily.com) 免费注册，每月有免费额度。

#### 第 2 步：编写维护提示词

复制 `templates/maintenance-prompt.md`，根据你的知识库领域修改：

- 替换文件列表为你的知识库文件
- 替换搜索关键词为你的领域关键词
- 调整更新格式与知识库风格一致

保存到 `~/.hermes/prompts/your-topic-maintenance.md`

#### 第 3 步：创建 cron 任务

```bash
hermes cron create \
  --name "知识库月度更新" \
  --schedule "0 0 1 * *" \
  --model "your-model" \
  --toolsets "web,file,terminal" \
  --prompt-file ~/.hermes/prompts/your-topic-maintenance.md \
  --deliver "weixin:your-channel-id"
```

或在 Hermes 对话中直接说：

> "创建一个每月1号凌晨运行的 cron 任务，模型用 XXX，工具集用 web+file+terminal，提示词从 ~/.hermes/prompts/your-topic-maintenance.md 读取，结果推送到微信。"

### 验证

创建后手动触发一次，确认搜索和文件更新正常：

```
hermes cron run <job_id>
```

查看运行状态：

```
hermes cron list
```

## 📋 工作流程

```
每月1号 00:00
    │
    ▼
┌─────────────┐
│  1. 确定时间  │  date 命令获取当前年月
│  范围        │  计算"上个月"的 YYYY-MM
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  2. 批量读取  │  read_file × N 并行读取
│  现有知识库  │  了解现有时间线/排名/里程碑
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  3. 并行搜索  │  web_search × M 并行搜索
│  最新信息    │  10-15个关键词覆盖主要方向
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  4. 筛选信息  │  ✅ 已确认发布 + 有日期 + 有名称
│             │  ❌ 排除传闻/预告/猜测
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  4.5 去重检查 │  ⚠️ 检查是否已存在
│             │  已有 → patch 更新 | 没有 → 新增
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  5. 更新文件  │  patch 精准编辑
│             │  时间线/排行榜/里程碑/日志
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  6. 验证     │  格式对齐/YAML完整/无重复
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  7. 输出摘要  │  推送到微信/Telegram
│             │  新增数/文件列表/搜索状态
└─────────────┘
```

## 🔧 核心设计要点

### 1. 并行操作（省 token、省时间）

```
❌ 错误：读文件1 → 读文件2 → 读文件3 → 搜索1 → 搜索2
✅ 正确：[读文件1, 读文件2, 读文件3] → [搜索1, 搜索2, 搜索3]
```

在同一个 assistant turn 里批量调用工具，大幅减少往返轮次。

### 2. patch 精准编辑（不覆盖全文）

```
❌ 错误：read_file → 修改内容 → write_file 覆盖整个文件
✅ 正确：read_file → 找到要改的位置 → patch old_string → new_string
```

大文件用 write_file 覆盖会浪费大量 token，且容易丢内容。

### 3. 去重检查（避免重复记录）

每月跑一次，如果上个月已加过某条记录，这个月可能重复添加。必须在新增前检查。

### 4. 搜索失败兜底

提示词中明确写出：如果 web_search 返回 401，在摘要中标注"搜索失败"，不要静默忽略。

## 🎯 领域配置示例

| 领域 | 搜索关键词示例 | 更新频率 |
|------|-------------|---------|
| AI 模型 | "AI model release YYYY-MM"、"OpenAI new model" | 每月 |
| 科技产品 | "smartphone release YYYY-MM"、"GPU announce" | 每月 |
| 金融投资 | "IPO YYYY-MM"、"merger acquisition YYYY-MM" | 每月 |
| 游戏发行 | "game release YYYY-MM"、"Steam new launch" | 每月 |
| 学术论文 | "breakthrough paper YYYY-MM"、"Nature Science publish" | 每月 |

详见 `templates/` 目录下的各领域配置示例。

## ⚠️ 踩坑记录

详见 [docs/troubleshooting.md](docs/troubleshooting.md)，包含：

- Tavily key 格式错误导致 401
- cron 任务工具集不加载 MCP 工具
- 微信限流导致 deliver 失败
- 模型 API 配额耗尽
- 搜索关键词过多导致 token 浪费

## 📄 License

MIT

## 🙏 致谢

- [Hermes Agent](https://hermes-agent.nousresearch.com) - AI Agent 框架
- [Obsidian](https://obsidian.md) - 知识管理工具
- [Tavily](https://tavily.com) - AI 搜索 API
