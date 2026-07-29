<div align="center">

**中文** · [English](./README.md)

# 🌌 Linear Style Illustration

**暗色发光的"AI 操作系统"系统图 —— 青绿×紫×淡紫双色调，胶囊形 SVG 节点，每张图只有一个发光"内核"。**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Examples](https://img.shields.io/badge/EXAMPLES-3-2ea44f?style=flat-square&labelColor=333)](./examples)
[![Stars](https://img.shields.io/github/stars/yanliudesign/linear-style-illustration?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/linear-style-illustration/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

一个"审美克制"的 skill，把任何系统 / 流程 / 架构想法变成**暗色、技术感的"AI 操作系统"风格图**——就是你在 Linear 发布会、AI Agent 产品 deck、技术官网首页里见到的那种图。标志性动作：**近黑背景** + **背景里柔和的模糊色块光晕** + **胶囊形节点，细描边** + **每张图恰好一个发光的"内核"节点**，用来标出重心所在。

不是通用画图工具，不是 Mermaid，不是白板导出图。这是一种收敛、克制的暗色科技图风格——输出为一个自包含的 HTML 文件（内联 SVG），可以直接放进幻灯片，或截图导出成 PNG。

<p align="center">
  <img src="./examples/01-hub-and-spoke.png" width="100%" alt="Hub and spoke diagram">
  <br><sub><b>Hub and spoke</b> —— 路由分发给多个专项 worker</sub>
</p>
<p align="center">
  <img src="./examples/02-state-machine.png" width="100%" alt="State machine diagram">
  <br><sub><b>State machine</b> —— 信心关卡决定下一步谁来处理</sub>
</p>
<p align="center">
  <img src="./examples/03-layered-stack.png" width="100%" alt="Layered stack diagram">
  <br><sub><b>Layered stack</b> —— 一个薄内核支撑起上层一切</sub>
</p>

## 目录

| 文件 | 作用 |
|---|---|
| [`SKILL.md`](./SKILL.md) | Skill 主入口 —— Claude 读它来判断何时触发、该用哪种构图 |
| [`references/style-tokens.md`](./references/style-tokens.md) | 可直接复制的 CSS/HTML/SVG：字体、`:root` 色彩变量、背景系统（网格/光晕/暗角）、文字组件、箭头 marker 定义、节点填充/描边配方 |
| [`references/patterns.md`](./references/patterns.md) | 7 种图表原型 —— 胶囊链、Hub-and-spoke、分层结构、汇聚漏斗、状态机、飞轮循环、编号瀑布流 —— 均为可直接改的 SVG/HTML 代码块 |
| [`examples/`](./examples/) | 3 张渲染好的示例图 + 对应源码 |

## 三条铁律

1. **永远近黑背景。** `--stage-bg: #06070a`。不允许白色卡片，不允许浅色模式。层次感来自淡淡的网格、模糊的色块光晕和暗角渐变——而不是每个节点都加投影。
2. **颜色是角色，不是装饰。** 青绿 = 主流程 / 成功 / AI 输出。紫色 = 次要 / 人类 / 决策。淡紫 = 第三类 / 组织结构。警告橙 = 关卡、暂停、需要人工介入。不要随便配色，一张图里最多用 2–3 种颜色。
3. **用胶囊，不用方框——只发一处光。** 节点是圆角的（端点用 `rx` = 高度的一半，卡片用 `rx 12–18`），低透明度填充 + 细描边。每张图只有一个"内核"节点会发光（drop-shadow 滤镜 + 实色描边）。最多 6–7 个节点，超过就拆成两张图。

## 安装

丢到 Claude Code 的 skills 目录：

```bash
git clone https://github.com/yanliudesign/linear-style-illustration.git \
  ~/.claude/skills/linear-style-illustration
```

重启 Claude Code。触发关键词见 [`SKILL.md`](./SKILL.md) 顶部。

## 触发关键词

| 你说 | 会触发 |
|---|---|
| *"给我做一张 Linear 风格的图"* / *"Linear-style diagram"* | 本 skill |
| *"暗色科技 / AI-OS 架构图"* | 本 skill |
| *"Hub-and-spoke 图"* / *"一个路由分发给多个 worker"* | 本 skill |
| *"带信心关卡的状态机图"* | 本 skill |
| *"分层架构图，中间是内核"* | 本 skill |
| *"深色科技图"* / *"暗色架构图"* | 本 skill |

## 适用

- **AI / Agent 产品 deck** —— 架构页、"它是怎么工作的"图解、协调者/工作者模式
- **技术官网首页** —— 暗色模式下的产品/功能图解、"内部原理"板块
- **技术分享 / 大会演讲** —— 系统图、状态机、飞轮循环
- **技术博客 / 文档** —— 需要在暗色背景上足够精致的架构图

## 什么时候**不要**用

- **浅色模式 / 打印文档** —— 这套配色依赖近黑背景才成立
- **数据可视化**（带真实数值坐标轴的图表）—— 这是系统/流程图风格，不是图表库
- **手绘 / 天马行空插画** —— 风格完全相反，这个是精确、技术、冷静的
- **组织架构图 / 密集的企业级图表**（15+ 节点）—— 这套风格上限在 6–7 个节点左右

## 交付格式

一次交付给你一个自包含的 `.html` 文件（内联 SVG，1600–1920px 画布），使用 `references/style-tokens.md` 里的样板代码 + `references/patterns.md` 里最贴近的原型——可以直接用浏览器打开、嵌进幻灯片，或截图导出 PNG。

## License

MIT — see [LICENSE](./LICENSE).
