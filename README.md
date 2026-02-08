# rss2wechat-n8n-workflow
基于 n8n 的工作流，可聚合多源 RSS 订阅，通过 AI 润色，自动生成微信公众号草稿。

# rss2wechat-n8n-workflow

[![n8n](https://img.shields.io/badge/n8n-Workflow-orange?style=flat&logo=n8n&logoColor=white)](https://n8n.io/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## 🚀 描述

这个项目是一个基于n8n的工作流，专为AI和科技爱好者或创业者设计。它聚合多个RSS订阅源的内容（专注于AI、科技和产品新闻），使用网络爬取工具和AI模型抓取并处理文章，将其提炼成简洁、可读的新闻简报，并附上原链接，然后自动生成微信公众号的草稿。

工作流利用AI过滤和润色内容，确保只保留最具价值的AI和科技新闻。非常适合自动化内容 curation 和发布到微信公众号。

## 📋 功能

- **RSS聚合**：从多个来源如Product Hunt、Stratechery和TestingCatalog拉取最新条目（每个来源限制10条以提高效率）。
- **内容爬取**：使用FireCrawl从RSS链接中获取完整文章内容。
- **AI润色**：使用DeepSeek AI代理将原始内容转换为精美的、可读的新闻简报（Markdown格式），专注于AI和科技价值。系统提示："我是一名AI领域创业者，你是我的秘书。我需要把从网站爬取的数据整理成可阅读的新闻简报，每个新闻下附上原链接。要精美可读性强。只保留最有价值的AI和科技新闻内容。"
- **格式化**：将Markdown转换为HTML，并将换行替换为`<br>`以在微信中正确渲染。
- **微信集成**：使用API在微信公众号中创建草稿，包括标题、作者、内容和缩略图媒体。
- **模块化设计**：使用n8n节点构建，便于自定义，包括merge、limit、aggregate和code节点用于数据处理。

## 🔧 要求

- **n8n**：与所用节点兼容的版本（例如n8n 1.x）。通过npm、Docker或云托管安装。
- **API凭证**：
  - **DeepSeek API**：用于AI语言模型（在"DeepSeek Chat Model2"节点中使用）。
  - **FireCrawl API**：用于爬取文章内容（在"Scrape A Url And Get Its Content"节点中使用）。
  - **微信公众号API**：用于创建草稿（在"Wechat Official Account Node3"和相关节点中使用）。
- **依赖**：所有节点来自n8n内置或社区包（例如`@n8n/n8n-nodes-langchain`、`n8n-nodes-wechat-offiaccount`、`n8n-nodes-firecrawl`）。
- **环境**：n8n的Node.js运行时；无需额外安装。

## 📥 安装和设置

1. **安装n8n**：
   - 按照官方[n8n安装指南](https://docs.n8n.io/getting-started/installation/)操作。
   - 示例通过npm：`npm install n8n -g` 然后 `n8n start`。

2. **导入工作流**：
   - 从`rss2wechat-n8n-workflow.json`复制JSON。
   - 在n8n UI中，转到**Workflows > Import from File/URL** 并粘贴/上传JSON。
   - 或者使用n8n CLI：`n8n import:workflow --input=rss2wechat-n8n-workflow.json`。

3. **配置凭证**：
   - 在n8n中，转到**Credentials** 并添加：
     - DeepSeek API：从[DeepSeek](https://platform.deepseek.com/)获取API密钥。
     - FireCrawl API：从[FireCrawl](https://firecrawl.dev/)获取API密钥。
     - 微信公众号：从[微信开发者平台](https://mp.weixin.qq.com/)获取App ID、Secret等。
   - 将这些分配到相应节点（例如"DeepSeek Chat Model2"、"Scrape A Url And Get Its Content"、"Wechat Official Account Node3"）。

4. **自定义（可选）**：
   - 通过复制RSS节点并连接到"Merge"节点来添加更多RSS源。
   - 在"Limit"节点中调整限制，或在"AI Agent2"中更新AI提示以改变内容焦点。
   - 在"Wechat Official Account Node3"中更新草稿参数（例如标题、作者）。

## 🛠️ 使用

1. **触发工作流**：
   - 手动：在n8n UI中点击"Test workflow"（连接到"When clicking 'Test workflow'"节点）。
   - 定时：添加Schedule节点或使用n8n的cron功能每日/每周运行。

2. **工作流流程**：
   - 获取并限制RSS订阅。
   - 合并并爬取完整内容。
   - AI处理成简报。
   - 聚合、格式化并发送到微信作为草稿。

3. **输出**：
   - 在您的微信公众号后台出现新草稿，准备审阅和发布。
   - 示例草稿标题："最新001"（可自定义）。

## ⚠️ 故障排除

- **API错误**：检查凭证有效性和速率限制（例如DeepSeek或FireCrawl配额）。
- **内容问题**：如果爬取失败，确保URL有效；FireCrawl处理大多数站点，但可能需要针对反爬措施调整。
- **微信草稿**：确保"thumb_media_id"在您的微信媒体库中存在（通过"Wechat Official Account Node1"获取）。
- **调试**：使用n8n的执行日志检查节点输出。

## 🤝 贡献

欢迎贡献！Fork仓库，对工作流JSON进行更改，并提交pull request。欢迎添加更多RSS源、AI模型或集成（例如其他平台如Twitter/X）的想法。

## 📄 许可

本项目采用MIT许可 - 详情见[LICENSE](LICENSE)文件。

## 🙏 致谢

- 使用[n8n](https://n8n.io/)构建自动化。
- AI由[DeepSeek](https://deepseek.com/)提供支持。
- 爬取通过[FireCrawl](https://firecrawl.dev/)实现。
- 微信集成使用n8n的官方节点。

如有问题，在GitHub上打开issue。
