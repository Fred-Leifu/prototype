---
name: inline-svg-diagram
description: |
  当用户需要生成流程图、泳道图、时序图、架构图、ER 图、组织结构图、状态图、甘特图等任何结构化图表时，优先使用内联 SVG 直接渲染。无需外部 API、无需安装依赖，纯代码生成，实时可预览。触发词：画图、流程图、泳道图、架构图、时序图、ER图、组织结构图、状态图、可视化、diagram、flowchart、swimlane。
license: MIT
compatibility: opencode
metadata:
  audience: developers
  category: diagram
---

# Inline SVG Diagram Generator

当用户需要生成任何结构化图表时，直接使用内联 SVG 渲染。此技能优先级高于 Mermaid、ProcessOn 等方案。

## 规则

1. **纯 SVG 渲染**：直接输出 `<svg>` 标签，不依赖外部图片、API 或工具
2. **一次成型**：SVG 必须完整自包含，所有样式内联在 `<style>` 或元素属性中
3. **中文友好**：支持中文文本，使用 `font-family="Microsoft YaHei, sans-serif"`
4. **配色专业**：使用精心搭配的色板（见下方），禁止默认黑白
5. **响应式**：SVG 设置 `viewBox` 而非固定宽高

## 通用色板

```svg
<!-- 专业配色方案 -->
主色:   #4A90D9   (蓝)
辅色:   #7B68EE   (紫)
强调:   #E8833A   (橙)
成功:   #52C41A   (绿)
危险:   #FF4D4F   (红)
背景:   #F8F9FC   (浅灰)
边框:   #DFE3E8
文本:   #1D1D1F
次文本: #6B7280
```

## 流程图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 600" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .box { fill: #4A90D9; rx: 6; }
      .diamond { fill: #E8833A; }
      .line { stroke: #6B7280; stroke-width: 2; fill: none; }
      .arrow { fill: #6B7280; }
      .text { fill: #fff; font-size: 14px; text-anchor: middle; dominant-baseline: central; }
      .text-dark { fill: #1D1D1F; font-size: 14px; text-anchor: middle; dominant-baseline: central; }
      .label { fill: #6B7280; font-size: 12px; text-anchor: middle; }
    </style>
    <marker id="arrow" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="8" markerHeight="8" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" class="arrow"/>
    </marker>
  </defs>
  <rect width="800" height="600" fill="#F8F9FC"/>
  <!-- title -->
  <text x="400" y="35" fill="#1D1D1F" font-size="20" font-weight="bold" text-anchor="middle">流程图标题</text>
  <!-- 开始 -->
  <rect x="325" y="60" width="150" height="46" class="box"/>
  <text x="400" y="83" class="text">开始</text>
  <!-- 箭头 -->
  <line x1="400" y1="106" x2="400" y2="146" class="line" marker-end="url(#arrow)"/>
  <!-- 步骤 -->
  <rect x="300" y="150" width="200" height="46" class="box"/>
  <text x="400" y="173" class="text">处理步骤</text>
  <line x1="400" y1="196" x2="400" y2="236" class="line" marker-end="url(#arrow)"/>
  <!-- 判断 -->
  <polygon points="400,240 480,290 400,340 320,290" class="diamond"/>
  <text x="400" y="290" class="text-dark" font-size="13">判断条件</text>
  <!-- 是 -->
  <line x1="480" y1="290" x2="560" y2="290" class="line" marker-end="url(#arrow)"/>
  <text x="520" y="280" class="label">是</text>
  <rect x="564" y="267" width="160" height="46" class="box" fill="#52C41A"/>
  <text x="644" y="290" class="text">处理</text>
  <!-- 否 -->
  <line x1="400" y1="340" x2="400" y2="390" class="line" marker-end="url(#arrow)"/>
  <text x="412" y="365" class="label">否</text>
  <rect x="300" y="394" width="200" height="46" class="box" fill="#E8833A"/>
  <text x="400" y="417" class="text">其他处理</text>
  <line x1="400" y1="440" x2="400" y2="480" class="line" marker-end="url(#arrow)"/>
  <!-- 结束 -->
  <rect x="325" y="484" width="150" height="46" class="box" fill="#6B7280"/>
  <text x="400" y="507" class="text">结束</text>
</svg>
```

## 泳道图（跨职能流程图）模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 500" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .swimlane-bg { fill: #F8F9FC; stroke: #DFE3E8; stroke-width: 1; }
      .swimlane-header { fill: #4A90D9; }
      .swimlane-text { fill: #fff; font-size: 14px; font-weight: bold; text-anchor: middle; dominant-baseline: central; }
      .step { fill: #fff; stroke: #4A90D9; stroke-width: 2; rx: 6; }
      .step-text { fill: #1D1D1F; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
      .line { stroke: #6B7280; stroke-width: 2; fill: none; }
      .arrow { fill: #6B7280; }
      .title { fill: #1D1D1F; font-size: 18px; font-weight: bold; text-anchor: middle; }
    </style>
    <marker id="arrow" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="8" markerHeight="8" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" class="arrow"/>
    </marker>
  </defs>
  <rect width="900" height="500" fill="#fff"/>
  <text x="450" y="25" class="title">业务流程图</text>
  <!-- Lane 1 -->
  <rect x="0" y="50" width="900" height="100" class="swimlane-bg"/>
  <rect x="0" y="50" width="120" height="100" class="swimlane-header"/>
  <text x="60" y="100" class="swimlane-text">角色A</text>
  <rect x="160" y="70" width="150" height="46" class="step"/>
  <text x="235" y="93" class="step-text">发起请求</text>
  <line x1="310" y1="93" x2="400" y2="93" class="line" marker-end="url(#arrow)"/>
  <!-- Lane 2 -->
  <rect x="0" y="150" width="900" height="100" class="swimlane-bg"/>
  <rect x="0" y="150" width="120" height="100" class="swimlane-header"/>
  <text x="60" y="200" class="swimlane-text">角色B</text>
  <rect x="404" y="177" width="150" height="46" class="step"/>
  <text x="479" y="200" class="step-text">审核处理</text>
  <line x1="554" y1="200" x2="640" y2="200" class="line" marker-end="url(#arrow)"/>
  <!-- Lane 3 -->
  <rect x="0" y="250" width="900" height="100" class="swimlane-bg"/>
  <rect x="0" y="250" width="120" height="100" class="swimlane-header"/>
  <text x="60" y="300" class="swimlane-text">角色C</text>
  <rect x="644" y="277" width="160" height="46" class="step"/>
  <text x="724" y="300" class="step-text">完成处理</text>
  <!-- 返回箭头 -->
  <line x1="724" y1="323" x2="724" y2="380" class="line" marker-end="url(#arrow)"/>
  <text x="736" y="355" class="step-text" font-size="11" fill="#E8833A">驳回</text>
  <line x1="724" y1="380" x2="235" y2="380" class="line" stroke-dasharray="6,3" marker-end="url(#arrow)"/>
  <text x="480" y="373" class="step-text" font-size="11" fill="#E8833A">退回修改</text>
</svg>
```

## 时序图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 500" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .actor-box { fill: #4A90D9; rx: 4; }
      .actor-text { fill: #fff; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
      .lifeline { stroke: #DFE3E8; stroke-width: 1.5; stroke-dasharray: 6,4; }
      .arrow-line { stroke: #1D1D1F; stroke-width: 1.5; fill: none; }
      .arrow-head { fill: #1D1D1F; }
      .msg-text { fill: #1D1D1F; font-size: 12px; }
      .self-arrow { fill: #E8833A; stroke: #E8833A; stroke-width: 1.5; }
      .title { fill: #1D1D1F; font-size: 18px; font-weight: bold; text-anchor: middle; }
      .alt-bg { fill: #FFF7E6; stroke: #FFD591; stroke-width: 1; rx: 4; }
      .alt-text { fill: #E8833A; font-size: 11px; }
    </style>
    <marker id="arrowHead" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" class="arrow-head"/>
    </marker>
  </defs>
  <rect width="800" height="500" fill="#fff"/>
  <text x="400" y="25" class="title">时序图标题</text>
  <!-- Actors -->
  <rect x="50" y="50" width="100" height="34" class="actor-box"/>
  <text x="100" y="67" class="actor-text">用户</text>
  <rect x="350" y="50" width="100" height="34" class="actor-box" fill="#7B68EE"/>
  <text x="400" y="67" class="actor-text">系统</text>
  <rect x="620" y="50" width="120" height="34" class="actor-box" fill="#52C41A"/>
  <text x="680" y="67" class="actor-text">数据库</text>
  <!-- Lifelines -->
  <line x1="100" y1="84" x2="100" y2="460" class="lifeline"/>
  <line x1="400" y1="84" x2="400" y2="460" class="lifeline"/>
  <line x1="680" y1="84" x2="680" y2="460" class="lifeline"/>
  <!-- Message 1 -->
  <line x1="100" y1="120" x2="390" y2="120" class="arrow-line" marker-end="url(#arrowHead)"/>
  <text x="250" y="113" class="msg-text" text-anchor="middle">1. 发送请求</text>
  <!-- Message 2 -->
  <line x1="400" y1="160" x2="670" y2="160" class="arrow-line" marker-end="url(#arrowHead)"/>
  <text x="535" y="153" class="msg-text" text-anchor="middle">2. 查询数据</text>
  <!-- Return -->
  <line x1="680" y1="195" x2="410" y2="195" class="arrow-line" stroke-dasharray="5,3" marker-end="url(#arrowHead)"/>
  <text x="545" y="188" class="msg-text" text-anchor="middle">返回结果</text>
  <!-- Self call -->
  <path d="M400,230 L430,230 L430,260 L410,260" class="self-arrow" fill="none" marker-end="url(#arrowHead)"/>
  <text x="435" y="250" class="msg-text" font-size="11">自处理</text>
  <!-- alt fragment -->
  <rect x="260" y="280" width="280" height="80" class="alt-bg"/>
  <text x="270" y="297" class="alt-text">alt [条件分支]</text>
  <line x1="270" y1="310" x2="530" y2="310" class="line" stroke="#FFD591"/>
  <text x="280" y="325" class="msg-text" font-size="11">成功流程</text>
  <line x1="330" y1="310" x2="395" y2="345" class="arrow-line" marker-end="url(#arrowHead)"/>
  <text x="280" y="350" class="msg-text" font-size="11">异常流程</text>
  <!-- Message 3 -->
  <line x1="400" y1="390" x2="110" y2="390" class="arrow-line" marker-end="url(#arrowHead)"/>
  <text x="250" y="383" class="msg-text" text-anchor="middle">3. 返回响应</text>
</svg>
```

## 系统架构图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 600" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .layer-bg { fill: #F0F5FF; stroke: #D6E4FF; stroke-width: 1; rx: 8; }
      .layer-text { fill: #1D1D1F; font-size: 15px; font-weight: bold; }
      .module { fill: #fff; stroke: #4A90D9; stroke-width: 2; rx: 6; }
      .module-fill { fill: #4A90D9; rx: 6; }
      .module-text { fill: #1D1D1F; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
      .module-text-light { fill: #fff; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
      .arrow-line { stroke: #BFBFBF; stroke-width: 2; fill: none; }
      .arrow-head { fill: #BFBFBF; }
      .title { fill: #1D1D1F; font-size: 20px; font-weight: bold; text-anchor: middle; }
    </style>
    <marker id="arrowG" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" class="arrow-head"/>
    </marker>
  </defs>
  <rect width="900" height="600" fill="#F8F9FC"/>
  <text x="450" y="30" class="title">系统架构图</text>
  <!-- Layer 1: 接入层 -->
  <rect x="30" y="60" width="840" height="100" class="layer-bg"/>
  <text x="50" y="85" class="layer-text">接入层</text>
  <rect x="60" y="100" width="160" height="40" class="module-fill"/>
  <text x="140" y="120" class="module-text-light">Nginx 网关</text>
  <rect x="260" y="100" width="160" height="40" class="module"/>
  <text x="340" y="120" class="module-text">CDN</text>
  <rect x="460" y="100" width="160" height="40" class="module"/>
  <text x="540" y="120" class="module-text">负载均衡</text>
  <rect x="660" y="100" width="160" height="40" class="module"/>
  <text x="740" y="120" class="module-text">WAF</text>
  <!-- arrows -->
  <line x1="450" y1="160" x2="450" y2="185" class="arrow-line" marker-end="url(#arrowG)"/>
  <!-- Layer 2 -->
  <rect x="30" y="190" width="840" height="100" class="layer-bg"/>
  <text x="50" y="215" class="layer-text">应用层</text>
  <rect x="60" y="230" width="190" height="40" class="module-fill" fill="#7B68EE"/>
  <text x="155" y="250" class="module-text-light">用户服务</text>
  <rect x="280" y="230" width="190" height="40" class="module" stroke="#7B68EE"/>
  <text x="375" y="250" class="module-text">订单服务</text>
  <rect x="500" y="230" width="190" height="40" class="module" stroke="#7B68EE"/>
  <text x="595" y="250" class="module-text">支付服务</text>
  <rect x="720" y="230" width="120" height="40" class="module"/>
  <text x="780" y="250" class="module-text">消息队列</text>
  <line x1="450" y1="290" x2="450" y2="315" class="arrow-line" marker-end="url(#arrowG)"/>
  <!-- Layer 3 -->
  <rect x="30" y="320" width="840" height="100" class="layer-bg"/>
  <text x="50" y="345" class="layer-text">数据层</text>
  <rect x="60" y="360" width="200" height="40" class="module-fill" fill="#52C41A"/>
  <text x="160" y="380" class="module-text-light">MySQL 主库</text>
  <rect x="290" y="360" width="200" height="40" class="module" stroke="#52C41A"/>
  <text x="390" y="380" class="module-text">Redis 缓存</text>
  <rect x="520" y="360" width="200" height="40" class="module" stroke="#52C41A"/>
  <text x="620" y="380" class="module-text">Elasticsearch</text>
  <rect x="750" y="360" width="90" height="40" class="module"/>
  <text x="795" y="380" class="module-text">OSS</text>
  <line x1="450" y1="420" x2="450" y2="445" class="arrow-line" marker-end="url(#arrowG)"/>
  <!-- Layer 4 -->
  <rect x="30" y="450" width="840" height="60" class="layer-bg"/>
  <text x="50" y="475" class="layer-text">基础设施</text>
  <rect x="120" y="465" width="150" height="30" class="module"/>
  <text x="195" y="480" class="module-text" font-size="11">Kubernetes</text>
  <rect x="310" y="465" width="150" height="30" class="module"/>
  <text x="385" y="480" class="module-text" font-size="11">Docker</text>
  <rect x="500" y="465" width="150" height="30" class="module"/>
  <text x="575" y="480" class="module-text" font-size="11">监控告警</text>
  <rect x="690" y="465" width="150" height="30" class="module"/>
  <text x="765" y="480" class="module-text" font-size="11">日志中心</text>
</svg>
```

## ER 图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 850 480" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .entity { fill: #E6F0FF; stroke: #4A90D9; stroke-width: 2; rx: 6; }
      .entity-text { fill: #1D1D1F; font-size: 14px; font-weight: bold; text-anchor: middle; }
      .field { fill: #fff; stroke: #DFE3E8; stroke-width: 1; }
      .field-text { fill: #1D1D1F; font-size: 12px; }
      .pk-text { fill: #E8833A; font-size: 12px; font-weight: bold; }
      .fk-text { fill: #7B68EE; font-size: 12px; }
      .rel-line { stroke: #BFBFBF; stroke-width: 2; fill: none; }
      .rel-diamond { fill: #E8833A; }
      .title { fill: #1D1D1F; font-size: 18px; font-weight: bold; text-anchor: middle; }
    </style>
  </defs>
  <rect width="850" height="480" fill="#F8F9FC"/>
  <text x="425" y="25" class="title">E-R 关系图</text>
  <!-- Entity 1 -->
  <rect x="30" y="60" width="220" height="170" class="entity"/>
  <rect x="30" y="60" width="220" height="35" fill="#4A90D9" rx="6"/>
  <text x="140" y="82" fill="#fff" font-size="14" font-weight="bold" text-anchor="middle">用户</text>
  <rect x="40" y="105" width="200" height="28" class="field"/>
  <text x="50" y="123" class="pk-text">PK</text><text x="70" y="123" class="field-text">user_id</text>
  <rect x="40" y="137" width="200" height="28" class="field"/>
  <text x="50" y="155" class="field-text" fill="#999">　</text><text x="65" y="155" class="field-text">username</text>
  <rect x="40" y="169" width="200" height="28" class="field"/>
  <text x="50" y="187" class="field-text" fill="#999">　</text><text x="65" y="187" class="field-text">email</text>
  <rect x="40" y="201" width="200" height="28" class="field"/>
  <text x="50" y="219" class="field-text" fill="#999">　</text><text x="65" y="219" class="field-text">created_at</text>
  <!-- Entity 2 -->
  <rect x="550" y="60" width="240" height="170" class="entity"/>
  <rect x="550" y="60" width="240" height="35" fill="#52C41A" rx="6"/>
  <text x="670" y="82" fill="#fff" font-size="14" font-weight="bold" text-anchor="middle">订单</text>
  <rect x="560" y="105" width="220" height="28" class="field"/>
  <text x="570" y="123" class="pk-text">PK</text><text x="590" y="123" class="field-text">order_id</text>
  <rect x="560" y="137" width="220" height="28" class="field"/>
  <text x="570" y="155" class="fk-text">FK</text><text x="590" y="155" class="field-text">user_id</text>
  <rect x="560" y="169" width="220" height="28" class="field"/>
  <text x="570" y="187" class="field-text" fill="#999">　</text><text x="585" y="187" class="field-text">total_amount</text>
  <rect x="560" y="201" width="220" height="28" class="field"/>
  <text x="570" y="219" class="field-text" fill="#999">　</text><text x="585" y="219" class="field-text">status</text>
  <!-- Relationship -->
  <line x1="250" y1="130" x2="330" y2="130" class="rel-line"/>
  <line x1="550" y1="130" x2="470" y2="130" class="rel-line"/>
  <polygon points="340,120 360,130 340,140" class="rel-diamond"/>
  <text x="400" y="160" class="rel-line" font-size="13" text-anchor="middle" fill="#1D1D1F">拥有</text>
  <!-- cardinality -->
  <text x="290" y="123" class="field-text" fill="#E8833A" text-anchor="middle">1</text>
  <text x="510" y="123" class="field-text" fill="#E8833A" text-anchor="middle">N</text>
  <!-- Entity 3 -->
  <rect x="30" y="290" width="220" height="170" class="entity" stroke="#E8833A"/>
  <rect x="30" y="290" width="220" height="35" fill="#E8833A" rx="6"/>
  <text x="140" y="312" fill="#fff" font-size="14" font-weight="bold" text-anchor="middle">商品</text>
  <rect x="40" y="335" width="200" height="28" class="field"/>
  <text x="50" y="353" class="pk-text">PK</text><text x="70" y="353" class="field-text">product_id</text>
  <rect x="40" y="367" width="200" height="28" class="field"/>
  <text x="50" y="385" class="field-text" fill="#999">　</text><text x="65" y="385" class="field-text">product_name</text>
  <rect x="40" y="399" width="200" height="28" class="field"/>
  <text x="50" y="417" class="field-text" fill="#999">　</text><text x="65" y="417" class="field-text">price</text>
  <!-- Entity 4 -->
  <rect x="550" y="290" width="240" height="170" class="entity" stroke="#7B68EE"/>
  <rect x="550" y="290" width="240" height="35" fill="#7B68EE" rx="6"/>
  <text x="670" y="312" fill="#fff" font-size="14" font-weight="bold" text-anchor="middle">订单明细</text>
  <rect x="560" y="335" width="220" height="28" class="field"/>
  <text x="570" y="353" class="pk-text">PK</text><text x="590" y="353" class="field-text">detail_id</text>
  <rect x="560" y="367" width="220" height="28" class="field"/>
  <text x="570" y="385" class="fk-text">FK</text><text x="590" y="385" class="field-text">order_id</text>
  <rect x="560" y="399" width="220" height="28" class="field"/>
  <text x="570" y="417" class="fk-text">FK</text><text x="590" y="417" class="field-text">product_id</text>
  <!-- Rel 2 -->
  <line x1="250" y1="340" x2="330" y2="340" class="rel-line"/>
  <line x1="550" y1="340" x2="470" y2="340" class="rel-line"/>
  <polygon points="340,330 360,340 340,350" class="rel-diamond"/>
  <text x="400" y="370" class="rel-line" font-size="13" text-anchor="middle" fill="#1D1D1F">包含</text>
  <text x="290" y="333" class="field-text" fill="#E8833A" text-anchor="middle">1</text>
  <text x="510" y="333" class="field-text" fill="#E8833A" text-anchor="middle">N</text>
  <!-- Rel 3 -->
  <line x1="140" y1="290" x2="140" y2="260" class="rel-line" stroke-dasharray="5,3"/>
</svg>
```

## 组织结构图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 860 520" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .ceo { fill: #4A90D9; rx: 8; }
      .dept { fill: #7B68EE; rx: 6; }
      .team { fill: #fff; stroke: #4A90D9; stroke-width: 1.5; rx: 4; }
      .text-light { fill: #fff; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
      .text-dark { fill: #1D1D1F; font-size: 12px; text-anchor: middle; dominant-baseline: central; }
      .line { stroke: #BFBFBF; stroke-width: 1.5; fill: none; }
      .title { fill: #1D1D1F; font-size: 18px; font-weight: bold; text-anchor: middle; }
    </style>
  </defs>
  <rect width="860" height="520" fill="#F8F9FC"/>
  <text x="430" y="25" class="title">组织结构图</text>
  <!-- CEO -->
  <rect x="330" y="50" width="200" height="40" class="ceo"/>
  <text x="430" y="70" class="text-light" font-size="15" font-weight="bold">CEO</text>
  <!-- Lines from CEO to Depts -->
  <line x1="430" y1="90" x2="430" y2="120" class="line"/>
  <line x1="130" y1="120" x2="730" y2="120" class="line"/>
  <line x1="130" y1="120" x2="130" y2="145" class="line"/>
  <line x1="430" y1="120" x2="430" y2="145" class="line"/>
  <line x1="730" y1="120" x2="730" y2="145" class="line"/>
  <!-- Dept heads -->
  <rect x="50" y="150" width="160" height="36" class="dept"/>
  <text x="130" y="168" class="text-light">技术部</text>
  <rect x="350" y="150" width="160" height="36" class="dept" fill="#52C41A"/>
  <text x="430" y="168" class="text-light">产品部</text>
  <rect x="650" y="150" width="160" height="36" class="dept" fill="#E8833A"/>
  <text x="730" y="168" class="text-light">市场部</text>
  <!-- Lines to teams -->
  <line x1="130" y1="186" x2="130" y2="215" class="line"/>
  <line x1="60" y1="215" x2="200" y2="215" class="line"/>
  <line x1="60" y1="215" x2="60" y2="240" class="line"/>
  <line x1="130" y1="215" x2="130" y2="240" class="line"/>
  <line x1="200" y1="215" x2="200" y2="240" class="line"/>
  <line x1="430" y1="186" x2="430" y2="240" class="line"/>
  <line x1="730" y1="186" x2="730" y2="240" class="line"/>
  <!-- Teams -->
  <rect x="30" y="245" width="80" height="30" class="team"/>
  <text x="70" y="260" class="text-dark">前端组</text>
  <rect x="130" y="245" width="80" height="30" class="team"/>
  <text x="170" y="260" class="text-dark">后端组</text>
  <rect x="220" y="245" width="80" height="30" class="team" stroke="#7B68EE"/>
  <text x="260" y="260" class="text-dark">运维组</text>
  <rect x="380" y="245" width="100" height="30" class="team" stroke="#52C41A"/>
  <text x="430" y="260" class="text-dark">需求分析</text>
  <rect x="680" y="245" width="100" height="30" class="team" stroke="#E8833A"/>
  <text x="730" y="260" class="text-dark">品牌推广</text>
</svg>
```

## 状态图模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 750 420" font-family="Microsoft YaHei, sans-serif">
  <defs>
    <style>
      .start { fill: #52C41A; }
      .state { fill: #E6F0FF; stroke: #4A90D9; stroke-width: 2; rx: 20; }
      .state-text { fill: #1D1D1F; font-size: 14px; text-anchor: middle; dominant-baseline: central; }
      .choice { fill: #fff; stroke: #E8833A; stroke-width: 2; }
      .end { fill: #FF4D4F; }
      .line { stroke: #6B7280; stroke-width: 1.5; fill: none; }
      .arrow { fill: #6B7280; }
      .label { fill: #6B7280; font-size: 11px; }
      .title { fill: #1D1D1F; font-size: 18px; font-weight: bold; text-anchor: middle; }
    </style>
    <marker id="arrowS" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" class="arrow"/>
    </marker>
  </defs>
  <rect width="750" height="420" fill="#F8F9FC"/>
  <text x="375" y="25" class="title">订单状态流转图</text>
  <circle cx="375" cy="65" r="12" class="start"/>
  <!-- initial -->
  <line x1="387" y1="65" x2="420" y2="65" class="line" marker-end="url(#arrowS)"/>
  <rect x="300" y="90" width="150" height="40" class="state"/>
  <text x="375" y="110" class="state-text">待付款</text>
  <line x1="375" y1="130" x2="375" y2="170" class="line" marker-end="url(#arrowS)"/>
  <text x="385" y="152" class="label">支付</text>
  <rect x="300" y="175" width="150" height="40" class="state"/>
  <text x="375" y="195" class="state-text">待发货</text>
  <line x1="375" y1="215" x2="375" y2="255" class="line" marker-end="url(#arrowS)"/>
  <text x="385" y="237" class="label">发货</text>
  <rect x="300" y="260" width="150" height="40" class="state"/>
  <text x="375" y="280" class="state-text">运输中</text>
  <line x1="375" y1="300" x2="375" y2="335" class="line" marker-end="url(#arrowS)"/>
  <!-- choice -->
  <polygon points="375,340 390,352 375,364 360,352" class="choice"/>
  <text x="375" y="355" class="label" font-size="10">签收?</text>
  <line x1="390" y1="352" x2="480" y2="320" class="line" marker-end="url(#arrowS)"/>
  <text x="440" y="315" class="label" fill="#52C41A">是</text>
  <rect x="480" y="300" width="150" height="40" class="state" stroke="#52C41A"/>
  <text x="555" y="320" class="state-text" fill="#52C41A">已完成</text>
  <circle cx="675" cy="320" r="12" class="end"/>
  <line x1="630" y1="320" x2="663" y2="320" class="line" marker-end="url(#arrowS)"/>
  <line x1="360" y1="364" x2="220" y2="300" class="line" marker-end="url(#arrowS)"/>
  <text x="280" y="315" class="label" fill="#FF4D4F">否</text>
  <rect x="80" y="285" width="140" height="40" class="state" stroke="#FF4D4F"/>
  <text x="150" y="305" class="state-text" fill="#FF4D4F">已退回</text>
</svg>
```

## 输出要求

1. 每次输出**必须包含**完整的 `<svg>...</svg>` 代码块，并附带 Markdown 的 ````svg ```` 标记
2. SVG 必须自包含，不引用外部资源
3. 根据图表类型选择合适的模板，调整节点数和内容
4. 中文使用 `Microsoft YaHei` 字体，英文数字使用 `Arial`
5. 颜色使用上方色板，确保对比度良好
6. 复杂图表添加图例或标注说明
