---
title: Obsidian 中文资源指南
created: 2026-06-15
updated: 2026-06-15
type: guide
tags: [obsidian, guide, tools]
---

# 📘 Obsidian 中文资源指南

> 专为中文用户整理的 Obsidian 使用指南，涵盖插件推荐、快捷键、技巧和资源。  
> 本知识库就是基于这些最佳实践构建的。

---

## 1️⃣ 核心快捷键（必背）

| 快捷键 | 功能 | 使用场景 |
|--------|------|---------|
| `Ctrl + O` | 快速打开笔记 | 最常用的快捷键！ |
| `Ctrl + Shift + F` | 全局搜索 | 搜索所有笔记内容 |
| `Ctrl + G` | 打开图谱视图 | 查看笔记关系网络 |
| `Ctrl + P` | 命令面板 | 执行任何 Obsidian 操作 |
| `Ctrl + E` | 切换编辑/阅读模式 | 快速切换 |
| `Ctrl + Shift + E` | 导出为 PDF | 分享笔记 |
| `Ctrl + Click` | 在新标签页打开链接 | 不离开当前页面 |
| `Ctrl + Shift + Click` | 在右侧打开链接 | 分屏对比 |
| `Alt + ←` / `Alt + →` | 前进/后退 | 导航历史 |
| `Ctrl + ,` | 打开设置 | 快速调整配置 |

---

## 2️⃣ 必装插件推荐

### 🔥 核心插件（已安装或强烈推荐）

| 插件 | 用途 | 安装方式 | 状态 |
|------|------|---------|------|
| **Smart Connections** | AI 语义搜索，推荐相似笔记 | 社区插件 | ✅ 已安装 |
| **Dataview** | 笔记数据库，动态查询 | 社区插件 | ⭐ 强烈推荐 |
| **Templater** | 高级模板，自动插入变量 | 社区插件 | ⭐ 强烈推荐 |
| **Calendar** | 日历视图，配合 Daily Note | 社区插件 | ⭐ 推荐 |
| **Periodic Notes** | 周期性笔记（周/月/年） | 社区插件 | ⭐ 推荐 |
| **Kanban** | 看板视图，任务管理 | 社区插件 | ⭐ 推荐 |
| **Excalidraw** | 手绘风格图表 | 社区插件 | 可选 |
| **Mermaid Tools** | 流程图/时序图 | 已内置 | ✅ 自带 |

### 📝 编辑增强插件

| 插件 | 用途 | 安装方式 |
|------|------|---------|
| **Editor Syntax Highlight** | 代码高亮 | 社区插件 |
| **Table Editor** | 可视化表格编辑 | 社区插件 |
| **Paste URL into selection** | 粘贴链接自动转 Markdown | 社区插件 |
| **Image Auto Upload** | 图片自动上传到图床 | 社区插件 |
| **Note Refactor** | 笔记拆分/重组 | 社区插件 |

### 🔗 链接与导航插件

| 插件 | 用途 | 安装方式 |
|------|------|---------|
| **Breadcrumbs** | 面包屑导航，层级关系 | 社区插件 |
| **Supercharged Links** | 链接样式增强 | 社区插件 |
| **Graph Analysis** | 图谱分析工具 | 社区插件 |

---

## 3️⃣ 本知识库使用的最佳实践

### YAML Frontmatter 规范

每个笔记顶部使用标准 YAML 格式：

```yaml
---
title: 笔记标题
created: 2026-06-15
updated: 2026-06-15
type: index | entity | guide | log | review
tags: [tag1, tag2, tag3]
---
```

| 字段 | 说明 | 可选值 |
|------|------|--------|
| `title` | 笔记标题 | 任意文本 |
| `created` | 创建日期 | YYYY-MM-DD |
| `updated` | 更新日期 | YYYY-MM-DD |
| `type` | 笔记类型 | `index` 索引、`entity` 实体、`guide` 指南、`log` 日志、`review` 评测 |
| `tags` | 标签数组 | 见 [[00 - 标签索引]] |

### 文件命名规范

| 文件类型 | 命名格式 | 示例 |
|---------|---------|------|
| 首页/导航 | `00 - 名称.md` | `00 - 首页.md` |
| 索引页 | `00 - 名称.md` | `00 - 分类导航.md` |
| 日志 | `00 - 名称.md` | `00 - 更新日志.md` |
| 普通笔记 | `标题.md` | `OpenAI.md` |
| 分类笔记 | `领域名称.md` | `通用大模型公司.md` |
| 模板 | `Templates/模板名.md` | `Templates/公司笔记模板.md` |

### 文件夹结构建议

```
AI Knowledge Base/
├── .obsidian/          # 配置和插件
├── 00 - 首页.md        # 总入口
├── 00 - 分类导航.md     # 分类索引
├── 00 - 标签索引.md     # 标签聚合
├── 00 - 更新日志.md     # 更新记录
├── [各笔记文件].md      # 主要内容
├── Templates/          # 笔记模板
│   ├── 公司笔记模板.md
│   ├── 模型评测模板.md
│   └── 每日动态.md
├── Attachments/        # 图片、附件
│   └── [logo图片].png
└── Daily/             # 每日动态（可选）
    └── 2026-06-15.md
```

---

## 4️⃣ Markdown 语法速查

### 基础语法

```markdown
# 标题1
## 标题2
### 标题3

**粗体**  *斜体*  ~~删除线~~

- 无序列表
- 列表项
  - 子列表

1. 有序列表
2. 列表项

> 引用块

`行内代码`

```代码块
多行代码
```

[链接文字](URL)
![图片说明](图片路径)

| 表头1 | 表头2 |
|-------|-------|
| 内容1 | 内容2 |
```

### Obsidian 特有语法

```markdown
[[笔记名]]          # 双向链接
[[笔记名#标题]]      # 链接到具体标题
[[笔记名|显示文字]]   # 自定义显示文字

#标签名             # 标签（可用空格标签：#标签 名）

```mermaid
graph TD
    A[开始] --> B[结束]  # Mermaid 图表
```
```

---

## 5️⃣ 高级技巧

### 使用 Dataview 做动态查询

安装 Dataview 插件后，可以创建动态表格：

```dataview
TABLE title, type, updated
FROM "AI Knowledge Base"
WHERE type = "entity"
SORT updated DESC
```

### 使用 Templater 自动化

在模板中使用动态变量：

```markdown
---
title: <% tp.file.title %>
created: <% tp.date.now("YYYY-MM-DD") %>
updated: <% tp.date.now("YYYY-MM-DD") %>
---
```

### 使用 Callout 美化提示

```markdown
> [!info] 提示信息
> 这是重要的提示内容

> [!warning] 注意事项
> 这是警告内容

> [!tip] 小技巧
> 这是实用技巧
```

---

## 6️⃣ 中文资源推荐

### 社区与论坛
- **Obsidian 中文论坛**：https://forum-zh.obsidian.md
- **Obsidian 中文 Discord**：搜索相关社区
- **知乎话题**：Obsidian 笔记/知识管理
- **B站教程**：搜索 "Obsidian 教程"

### 推荐主题
| 主题名 | 特点 | 安装方式 |
|--------|------|---------|
| **Minimal** | 简洁美观，高度可定制 | 社区主题 |
| **Things** | 类 Things 3 风格 | 社区主题 |
| **AnuPpuccin** | 配色丰富 | 社区主题 |
| **Blue Topaz** | 国产主题，功能丰富 | 社区主题 |
| **Border** | 现代风格 | 社区主题 |

### 推荐中文博客/教程
- 搜索："Obsidian 知识库搭建"、"Obsidian PARA 方法"
- 推荐方法：PARA 方法（Projects, Areas, Resources, Archives）
- 推荐方法：Zettelkasten 卡片盒笔记法
- 推荐方法：MOC（Map of Content）内容地图 ← **本知识库使用的方法**

---

## 7️⃣ 常见问题

### Q1：如何备份知识库？
**答**：直接复制整个 `AI Knowledge Base` 文件夹到其他地方即可。推荐：
- 定期复制到网盘（WPS、夸克、OneDrive）
- 使用 Git 版本管理（高级用户）
- 开启 Obsidian Sync（付费，跨设备同步）

### Q2：如何跨设备使用？
**答**：
1. 将知识库文件夹放在云盘同步文件夹内（如 WPSDrive、OneDrive）
2. 或使用 Obsidian Sync（官方付费同步）
3. 手机端：Obsidian 手机 App 打开同一文件夹

### Q3：Smart Connections 插件没反应？
**答**：首次使用需要建立索引，可能需要几分钟。确保：
- 插件已启用
- 有充足的笔记内容（10+ 笔记效果更好）
- 右键菜单或命令面板中触发 "Smart Connections: Find"

### Q4：如何插入图片？
**答**：
- 直接粘贴：图片会自动保存到 `Attachments` 文件夹
- 拖拽图片到笔记中
- 设置中可配置默认附件路径：`设置 → 文件与链接 → 附件默认路径 → 指定的文件夹（Attachments/）`

### Q5：笔记太多找不到？
**答**：使用本知识库的 MOC 体系：
1. 先看 [[00 - 首页]] 快速入口
2. 查看 [[00 - 分类导航]] 分类索引
3. 使用 `Ctrl + O` 快速搜索笔记名
4. 使用 `Ctrl + Shift + F` 全局搜索内容
5. 使用 Smart Connections 发现相关笔记

---

*本指南持续更新，如有遗漏请随时补充！* 📝
