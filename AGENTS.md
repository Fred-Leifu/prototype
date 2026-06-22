# Global Rules

以下规则对所有对话任务生效，无需重复声明。

## 1. 严禁编造

一步步思考。在给出最终答案前，列出使用的具体证据或推理步骤。每一个事实性陈述都必须有源材料中的原文引用或明确出处作为支撑。

## 2. 拒绝发散

如果对回答的准确性置信度低于90%，请明确说明不确定性，并解释缺少哪些信息。准确性优先于完整性，宁可少说，不可错说。

## 3. 引用验证

关键事实必须附带原文引用。

## 4. 自我审查

在输出最终回复前，请根据原始提示词和源材料审查你的草稿。检查：
1. 幻觉（源材料中不存在的事实）
2. 逻辑错误
3. 违反指令的情况

如发现任何问题，请在显示最终结果前进行修正。

---

# 擎科生物 - 销综系统原型

纯前端 HTML/CSS/JS 原型，无框架依赖。内联页面（无 iframe 子页面）。

## 启动与部署

```bash
npm start              # 启动本地服务器，端口 3456
npm run deploy         # 部署到 GitHub Pages
# 或双击 start.bat     # 启动服务器并打开浏览器

部署到 GitHub Pages（使用 `deploy.js` 通过 GitHub API 自动部署），也可在页面内点击「发布」一键部署

## 页面架构

- **index.html** — 主外壳（Axure 风格导航 + 需求概览 + V1版本业务场景&流程 + 回收站 + 部署弹窗）
- 所有页面为内联 `div.page-content`，通过 `showPage()` 控制显隐

## 页面列表

| 导航路径 | pageName | 类型 |
|----------|----------|------|
| 需求概览 > 项目简介-简介 | overview-intro | 内联 |
| 需求概览 > 项目简介-修订记录 | overview-revision | 内联 |
| 需求概览 > 项目简介-历史数据 | overview-history | 内联 |
| 需求概览 > 项目简介-上线风险 | overview-risk | 内联 |
| 需求概览 > 项目简介-验收重点 | overview-acceptance | 内联 |
| 需求正文 > 业务场景&流程 > V1版本业务场景&流程 | scene-v1 | 内联 |
| 回收站 | recycle | 内联 |

## 技术约束

- **无框架**：纯 JavaScript，不使用 Vue/React 等
- **样式**：CSS 变量主题化，玻璃态效果
- **字体**：Google Fonts Inter（UI）+ JetBrains Mono（日志）
- **部署**：GitHub Pages（deploy.js 通过 GitHub API 自动部署，需 `GH_TOKEN` 或 `.github/token`）
- **仓库**：https://github.com/Fred-Leifu/prototype（已公开）

## OpenCode 技能

`.opencode/skills/` 已配置用于 AI 辅助开发的技能：图片识别、内联 SVG 图表、PaddleOCR、ProcessOn 图表。

## 常用操作

- 添加新页面：在 `index.html` 新增 `div#page-{name}.page-content`，并在 `showPage()` 的 `titles` 中添加映射，在 `axure-nav` 中添加导航项
- 样式调整：修改 `styles.css`
- 部署：`npm run deploy`（或页面内点击「发布」）
