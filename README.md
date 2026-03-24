# AI资讯收集器 (AI News Collector)

[![Version](https://img.shields.io/badge/version-v1.0.0-blue.svg)](https://github.com/tincotian-byte/ai-news-collector-skill/releases)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

自动从网络搜索获取最新AI动态信息，整合国内外AI大厂及研究机构资讯。

## 功能特点

- **自动采集**: 从OpenAI、Anthropic、DeepSeek、阿里千问等国内外AI大厂获取最新动态
- **智能处理**: 自动去重、中文翻译、趋势总结
- **本地存储**: 按日期生成Markdown格式简报
- **可视化界面**: 蓝白配色的HTML阅读器，支持多维度筛选
- **信源可配置**: 用户可自定义编辑资讯来源

---

## 安装说明

本 Skill 同时支持 **QoderWork** 和 **Claude** 两种 AI 工具。

### QoderWork 安装

#### 方式一：直接下载（推荐）

1. 访问 [GitHub Releases](https://github.com/tincotian-byte/ai-news-collector-skill/releases) 页面
2. 下载最新版本的 `ai-news-collector-skill.zip`
3. 解压到 QoderWork 的 skills 目录：
   - **Windows**: `%USERPROFILE%\.qoderwork\skills\`
   - **macOS/Linux**: `~/.qoderwork/skills/`

#### 方式二：Git 克隆

```bash
git clone https://github.com/tincotian-byte/ai-news-collector-skill.git

# Windows
copy ai-news-collector-skill %USERPROFILE%\.qoderwork\skills\ai-news-collector\

# macOS/Linux
cp -r ai-news-collector-skill ~/.qoderwork/skills/ai-news-collector/
```

#### 验证安装

重启 QoderWork，对 AI 助手说：`"收集今天的AI资讯"`

---

### Claude 安装

#### 方式一：Claude 客户端安装（推荐）

1. 打开 Claude 客户端，进入 **Settings** → **Skills**
2. 点击 **Install Skill** 或 **Add Skill**
3. 选择 **From GitHub** 或 **From URL**
4. 输入仓库地址：`https://github.com/tincotian-byte/ai-news-collector-skill`
5. 点击安装，等待完成

#### 方式二：手动安装

1. 下载本仓库的 ZIP 文件并解压
2. 打开 Claude 客户端，进入 **Settings** → **Skills**
3. 点击 **Install from Folder**
4. 选择解压后的 `ai-news-collector-skill` 文件夹
5. 重启 Claude 客户端

#### 方式三：Claude Web 版（claude.ai）

1. 访问 [claude.ai](https://claude.ai)
2. 点击左下角 **Settings** → **Skills**
3. 点击 **+ Add Skill**
4. 粘贴 GitHub 仓库地址：`https://github.com/tincotian-byte/ai-news-collector-skill`
5. 点击 **Install**

#### 验证安装

在 Claude 对话中输入：`"收集今天的AI资讯"` 或 `"获取最新AI动态"`

如果 Skill 正常加载，Claude 会开始搜索并生成简报。

---

### 通用手动安装（任意 AI 工具）

如果上述方式不适用：

1. 下载本仓库源码
2. 找到你的 AI 工具的 skills 目录（通常名为 `.skills`、`skills` 或 `agents/skills`）
3. 将本文件夹复制到该目录下，重命名为 `ai-news-collector`
4. 重启 AI 工具
5. 测试指令：`"收集今天的AI资讯"`

---

## 使用流程

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  用户指令   │ → │  自动采集   │ → │  本地存储   │ → │  随时调阅   │
│ 收集AI资讯  │    │ 搜索+去重   │    │ MD+HTML     │    │ 筛选+展示   │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

### 1. 发起采集（用户驱动）

对 AI 助手说出指令，触发自动采集：

| 指令示例 | 说明 |
|---------|------|
| `"收集今天的AI资讯"` | 采集最近一周的AI动态 |
| `"获取最新AI动态"` | 同上 |
| `"生成AI新闻简报"` | 同上 |

**采集逻辑**：
- 默认采集最近一周的AI新闻
- 若距上次采集不到7天，仅采集增量内容（避免重复）
- 自动去重：同一事件多个信源只保留最权威的一条
- 智能识别：区分"文章发布时间"和"事件实际发生时间"

### 2. 本地存储（自动生成）

采集完成后，Skill 自动在工作目录生成以下文件：

```
workspace/
├── news/
│   └── 2026-03-23.md          # Markdown格式新闻简报
├── sources.json                # 信源配置文件（可编辑）
└── index.html                  # HTML阅读器（数据已嵌入）
```

**Markdown 简报内容**：
- 采集日期和统计信息
- AI趋势总结（基于本次采集）
- 重点资讯列表（标题、来源、时间、摘要、要点）
- 全部资讯清单

### 3. 随时调阅（本地展示）

双击打开 `index.html`，即可浏览所有历史资讯：

**功能特性**：
- **时间筛选**：今天 / 最近一周 / 最近一个月 / 最近一年 / 自定义
- **趋势总结**：根据时间范围自动聚合，最多显示4条关键趋势
- **多维筛选**：厂商、技术领域、优先级（支持多选，动态计数）
- **视图切换**：完整视图 / 紧凑视图
- **离线可用**：所有数据嵌入HTML，无需网络即可查看

**使用示例**：
1. 想查看最近一周的AI动态 → 点击顶部"最近一周"Tab
2. 想关注某个厂商的资讯 → 左侧勾选对应厂商
3. 想看高优先级新闻 → 左侧勾选"高优先级"

---

## 自定义配置

### 编辑信源

编辑工作目录下的 `sources.json` 文件：

```json
{
  "sources": [
    {
      "name": "OpenAI",
      "category": "国际AI大厂",
      "tier": 1,
      "enabled": true,
      "urls": ["openai.com/blog"],
      "keywords": ["OpenAI", "GPT"],
      "note": "GPT系列"
    }
  ]
}
```

- `enabled`: 设为 `false` 可禁用该信源
- 在 `sources` 数组中添加新条目可增加信源

---

## 支持的资讯来源

### 国际大厂
- OpenAI (GPT系列、产品更新)
- Anthropic (Claude系列)
- Google DeepMind (Gemini系列)
- Microsoft AI
- Meta AI
- xAI
- NVIDIA

### 国内大厂
- 阿里通义千问
- 百度文心一言
- 字节跳动豆包
- 腾讯混元
- 智谱AI (ChatGLM)
- 月之暗面Kimi
- DeepSeek
- MiniMax
- 百川智能
- 零一万物
- 阶跃星辰

### 研究机构
- AI2、Stanford HAI、MIT CSAIL
- Berkeley AI Research
- 清华AIR

### 权威媒体
- 机器之心、量子位、36氪、雷峰网
- TechCrunch、The Verge、VentureBeat

---

## 文件结构

```
workspace/
├── news/                    # 每日资讯MD文件
│   ├── 2026-03-23.md
│   └── ...
├── sources.json             # 信源配置（用户可编辑）
└── index.html               # 阅读器主页面
```

---

## HTML 阅读器功能

- **时间筛选**: 今天 / 最近一周(默认) / 最近一个月 / 最近一年 / 自定义
- **趋势总结**: 基于时间范围自动聚合，最多显示4条，支持高亮
- **侧栏筛选**: 厂商、技术领域、优先级（动态计数）
- **视图切换**: 完整视图 / 紧凑视图

---

## 更新日志

### v1.0.0 (2026-03-23)
- 初始版本发布
- 支持国内外主要AI厂商资讯采集
- 内置HTML阅读器，支持时间筛选和趋势总结
- 可配置信源（sources.json）
- 智能去重和事件时间校验

---

## 贡献指南

欢迎提交 Issue 和 PR！

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

---

## 许可证

[MIT](LICENSE) © 2026 AI News Collector Team
