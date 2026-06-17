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

# 擎科生物 - 销综系统账单管理原型

纯前端 HTML/CSS/JS 原型，无框架依赖。

## 启动与部署

```bash
npm start              # 启动本地服务器，端口 3456
npm run deploy         # 部署到 GitHub Pages
# 或双击 start.bat     # 启动服务器并打开浏览器

部署到 GitHub Pages（使用 `deploy.js` 通过 GitHub API 自动部署），也可在页面内点击「发布」一键部署

## 页面架构

- **index.html** — 主外壳（导航 + 侧面板 + 需求概览），通过 `<iframe>` 嵌入子页面
- **子页面通信**：`window.postMessage()` 桥接 iframe → 父页面（打开侧面板、调整高度）
- **unbilled.html** — 未出账账单（3 维度标签页：单位/课题组/客户 + 侧面板订单详情 + 分页）
- **reconciliation.html** — 对账单（同上 + 行首复选框列）
- **config.html** — 对账要求配置（课题组列表 CRUD + 侧面板修改 + 修改记录弹窗）

子页面通过 `/styles.css` 共享样式。

## 技术约束

- **无框架**：纯 JavaScript，不使用 Vue/React 等
- **样式**：2045 行 CSS，CSS 变量主题化，玻璃态效果
- **字体**：Google Fonts Inter（UI）+ JetBrains Mono（日志）
- **部署**：GitHub Pages（deploy.js 通过 GitHub API 自动部署，需 `GH_TOKEN` 或 `.github/token`）
- **仓库**：https://github.com/Fred-Leifu/prototype（已公开）
- **sidepanel DOM 在 index.html**，子页面通过 `postMessage` 请求打开，禁止在子页面内创建

## 需求文档

`docs/260601商务中心规划-账单.md` — PRD，定义了 V1-V5 版本规划
`docs/Prompt.txt` — 需求变更清单（RP-260616-0001 ~ 0007），追溯原型开发过程

## OpenCode 技能

`.opencode/skills/` 已配置用于 AI 辅助开发的技能：图片识别、内联 SVG 图表、PaddleOCR、ProcessOn 图表。

## 常用操作

- 新增页面/功能：在 `docs/Prompt.txt` 追加需求，AI 实现后提交
- 样式调整：修改 `styles.css`，页面级样式在各 html 的 `<style>` 中
- 侧面板逻辑：`index.html` 的 `openSidePanel()` / `closeSidePanel()`
