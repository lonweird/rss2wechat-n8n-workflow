# rss2wechat-n8n-workflow

[![n8n](https://img.shields.io/badge/n8n-Workflow-orange?style=flat&logo=n8n&logoColor=white)](https://n8n.io/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## 🚀 描述

一个基于n8n的工作流，可聚合多个RSS订阅源，使用网络爬取工具和AI模型抓取并处理文章，将其提炼成简洁、可读的新闻简报，然后发布到微信公众号的草稿箱。

## 📋 功能

- **RSS聚合**：从多个来源如Product Hunt、Stratechery和TestingCatalog拉取最新条目。
- **内容爬取**：使用FireCrawl从RSS链接中获取完整文章内容。
- **AI润色**：调用 AI Agent将原始内容转换为精美的、可读的新闻简报（Markdown格式）。
- **格式化**：将Markdown转换为HTML，并将换行替换为`<br>`以在微信中正确渲染。
- **微信集成**：使用API在微信公众号中创建草稿，包括标题、作者、内容和缩略图媒体。

## 🛠️ 使用


1。 **导入工作流**：

  - 从rss2wechat-n8n-workflow.json复制JSON。
  - 在n8n UI中，转到Workflows > Import from File/URL 并粘贴/上传JSON。

2. **触发工作流**：
- 手动：在n8n UI中点击"Test workflow"（连接到"When clicking 'Test workflow'"节点）。
- 定时：添加Schedule节点或使用n8n的cron功能每日/每周运行。

3. **工作流流程**：
- 获取并限制RSS订阅。
- 合并并爬取完整内容。
- AI处理成简报的格式。
- 聚合、格式化并发送到微信公众号作为草稿。

4. **输出**：
- 在您的微信公众号后台出现新草稿，准备审阅和发布。

## ⚠️ 故障排除

- **API错误**：检查凭证有效性和速率限制（例如DeepSeek或FireCrawl配额）。
- **内容问题**：如果爬取失败，确保URL有效；FireCrawl处理大多数站点，但可能需要针对反爬措施调整。
- **微信草稿**：确保"thumb_media_id"在您的微信媒体库中存在（通过"Wechat Official Account Node1"获取）。
- **调试**：使用n8n的执行日志检查节点输出。


如有问题，在GitHub上打开issue。
