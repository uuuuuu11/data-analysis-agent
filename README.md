# 数探｜智能数据分析 Agent

<p align="center">
  <img src="./static/Images/icon.png" alt="数探 Agent" width="112" />
</p>

<p align="center"><strong>把 Excel、数据库和业务 API 变成可追问、可验证、可交付的分析结果</strong></p>

<p align="center">
  <a href="./README_EN.md">English</a> ·
  <a href="./docs/数探-Data-Analysis-Agent-PRD-精简版.md">投递精简 PRD</a> ·
  <a href="./docs/数探-Data-Analysis-Agent-PRD.md">完整 PRD</a> ·
  <a href="./DEMO_GUIDE.md">5 分钟体验</a> ·
  <a href="./DEPLOYMENT.md">部署指南</a>
</p>

## 项目简介

数探是面向业务分析的对话式 AI 数据工作台。用户接入文件或数据源后，用自然语言提出问题；系统通过受控工具执行查询、清洗、统计和图表生成，并将数据范围、工具过程和结果放在同一会话中。

它解决的不是“让模型回答一个问题”，而是让不会 SQL 的业务人员完成一次可核验的数据分析：**添加数据 → 确认字段 → 提出问题 → 真实执行 → 查看依据 → 继续追问**。

![数探首页](./docs/images/homepage.png)

## 核心能力

| 能力 | 说明 |
| --- | --- |
| 对话式分析 | 使用中文或英文提出经营问题，支持连续追问、流式结果、停止与有限重试。 |
| 多源数据接入 | Excel/CSV、SQL 数据库、Google Sheets、HTTP API、本地工作区和示例数据。 |
| 可信执行 | 数据范围可见；SQL 只读校验；查询、统计、清洗和图表由工具执行。 |
| 分析与交付 | 数据质量、聚合、趋势、建模、预测、图表、Excel、报告、PPT 和 Dashboard。 |
| 分析资产复用 | 历史会话、个人知识库、指标口径、业务规则和个人偏好。 |
| 长任务管理 | 解析、导出和长时分析可进入后台任务，支持查看状态、取消、恢复和下载。 |

## 为什么结果可核验

```mermaid
flowchart LR
    A[选择数据范围] --> B[自然语言提问]
    B --> C[Agent 规划]
    C --> D[受控工具执行]
    D --> E[表格、图表与结论]
    E --> F[追问、导出或保存]
```

- 大模型负责理解问题、组织步骤和解释结果；工具负责实际查询、计算与验证。
- 数值结论对应数据范围和工具结果；工具失败、数据不足或口径不清时展示真实状态。
- 个人知识库沉淀指标定义、业务规则和背景知识，避免每次重新解释口径。

## 快速开始

环境：Python 3.10+；修改前端时另需 Node.js 20.19+ 与 pnpm。

```powershell
git clone https://github.com/qrwuu/data-analysis-agent.git
cd data-analysis-agent

python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt

Copy-Item .env.example .env
python app.py
```

打开 <http://localhost:5001/>。完整部署、Docker 与生产配置见 [DEPLOYMENT.md](./DEPLOYMENT.md)。

## 模型服务配置

部署数探时，在服务端的 `.env` 文件中配置兼容的模型服务、模型名称和访问密钥，再启动应用。模型配置仅在部署环境生效，不会暴露给浏览器；用户无需在页面中填写模型地址或密钥。

## 文档与验证

| 文档 | 用途 |
| --- | --- |
| [投递精简 PRD](./docs/数探-Data-Analysis-Agent-PRD-精简版.md) | 10–15 页作品集阅读版本。 |
| [完整 PRD](./docs/数探-Data-Analysis-Agent-PRD.md) | 完整需求、验收、风险与评测口径。 |
| [架构说明](./ARCHITECTURE.md) | 系统模块、数据流与技术架构。 |
| [离线评测](./evals/README.md) | 冻结数据集、Prompt A/B、指标与复现实验。 |
| [安全策略](./SECURITY.md) | SQL、路径、浏览器和凭据安全基线。 |

```bash
python -m unittest discover -s Test -p "test_*.py" -v
```

## 数据与安全

- 模型与外部数据源凭据仅在部署环境配置。
- SQL 使用 AST 级只读校验，阻断写入和高风险语句。
- 工作区屏蔽 `.env`、`.git`、`.ssh`、私钥等敏感路径。
- 浏览器启用 CSP、同源写保护、内容类型保护和限制性权限策略。
