---
name: liquid-glass-web
description: 将现有或新建的 Web 界面设计成清透、分层、可读的液态玻璃风格，同时遵守项目原有布局和功能约定。Build or restyle Web interfaces with layered Liquid Glass-inspired CSS materials while preserving existing layout and behavior. Not for native Apple materials or general gesture animation work.
---

# 液态玻璃网页设计 / Liquid Glass Web Design

用 CSS 的透明填充、环境光、高光、模糊和阴影营造安静且可读的层次。它是受 Apple Liquid Glass 启发的 Web 表达，不等于 Apple 原生系统材质。

Use translucent fills, ambient light, highlights, blur, and shadow to create calm, legible depth. This is a Web interpretation inspired by Apple Liquid Glass, not the native system material.

来源 / Source: [基于 Codex+GPT6 快速开发 macOS 26 液态玻璃风格的 Web 界面](https://mp.weixin.qq.com/s/uyNplWJDvKcshM-jt-hpfg?scene=1). 文章中的演示功能和布局只是示例。 / The article's demo features and layouts are examples, not product requirements.

## 范围 / Scope

- 先阅读项目规则、现有组件、设计变量、页面和关键交互。只要求视觉改版时，保留路由、API、权限、数据含义和业务行为。 / Read project rules, components, tokens, pages, and key interactions first. For a visual-only request, preserve routes, APIs, permissions, data semantics, and business behavior.
- 沿用项目的组件和样式模式。用户明确指定的品牌色优先。不要将文章的搜索、收藏、弹窗、假数据或模拟进度复制到现有产品。 / Reuse the product's component and styling patterns. Explicit brand choices take precedence. Do not import the article's demo interactions or fake data.
- 遵守项目已有的响应式布局合同。文章中的手机横向导航只是示例；如果项目规定了导航的行数或结构，就保持该规定。 / Respect the product's responsive contract. The article's horizontal mobile navigation is only an example; preserve any required row count or structure.

## 视觉配方 / Visual recipe

以下数值是调参起点，须按真实内容和品牌调整。 / These are starting values to tune against real content and brand constraints.

| 用途 / Role | 起点 / Starting value |
| --- | --- |
| 页面 / Page | `#F7F9FC` |
| 左侧暖杏环境光 / Warm left light | `#FFD29D` |
| 右侧冷蓝环境光 / Cool right light | `#A0CFFF` |
| 主操作 / Primary action | `#2868D8` |
| 正文 / Main text | `#202C40` |
| 次要文字 / Secondary text | `#5B6D85` |

环境色可从宽约 `70rem` 的径向渐变开始：暖光位于 `-8% 6%`、alpha 约 `.46`，冷光位于 `108% 9%`、alpha 约 `.50`；让中央阅读区保持干净。若色光干扰文字，先降低 alpha 或缩小范围。 / Start with broad radial gradients near the side edges, fading before the central reading area. Reduce opacity or reach when color competes with content.

表面由半透明白色填充、细高光边框、适度背景模糊和柔和阴影组成。白色覆盖与文字对比比增加 blur 更重要。只给背景颜色设置 alpha，不给含有文字和控件的父容器设置 `opacity`。 / Build each surface from translucent white fill, a fine highlight border, restrained backdrop blur, and soft shadow. White coverage and text contrast matter more than blur. Never fade an entire content container with parent `opacity`.

| 层级 / Surface | 白色覆盖 / White coverage | 模糊 / Blur |
| --- | ---: | ---: |
| 导航 / Navigation | ~42% | ~24px |
| 工具条 / Toolbar | ~58% | ~18px |
| 卡片 / Card | ~72% | often 0 |
| 弹窗 / Modal | ~86% | ~30px |
| 长文本 / Reading | ~96% | 0 |

避免大面积玻璃叠玻璃；内层输入框和按钮通常只需简单填充与细边框。高频操作页面保持紧凑、信息顺序稳定、主操作明确。文章中的间距阶梯为 8/12/16/24px，表面圆角约 18–22px，控件圆角约 10–12px；已有设计系统优先。 / Avoid large glass-on-glass stacks. Keep operational pages compact and scannable with stable information order and one clear primary action. Adapt spacing and radii to the existing design system.

CSS 起点：先提供实色底，再有条件地加玻璃效果。 / CSS starting point: provide a solid base before the conditional glass effect.

```css
.glass-surface {
  background: #f8fbff;
  border: 1px solid #d5deea;
}

@supports ((-webkit-backdrop-filter: blur(1px)) or (backdrop-filter: blur(1px))) {
  .glass-surface {
    background: linear-gradient(145deg, rgb(255 255 255 / 78%), rgb(255 255 255 / 42%));
    border: 1px solid rgb(255 255 255 / 82%);
    box-shadow: inset 0 1px 0 rgb(255 255 255 / 84%), 0 18px 48px rgb(55 83 118 / 14%);
    -webkit-backdrop-filter: blur(24px) saturate(130%);
    backdrop-filter: blur(24px) saturate(130%);
  }
}
```

## 交互与适配 / Interaction and accessibility

- 看起来可点击的范围必须与真实命中区域、键盘操作、可见焦点和无障碍名称一致；必要时优先使用原生控件。 / Match visual affordance to the actual hit area, keyboard behavior, visible focus, and accessible name; prefer native controls where appropriate.
- 用同一材质系统呈现已有的默认、加载、禁用、错误、成功和取消状态，不合并不同的业务状态。 / Style existing idle, loading, disabled, error, success, and cancel states consistently without merging distinct business states.
- 桌面、平板和手机应按项目约定重排，保留重要状态与操作，维持合理触控面积并避免整页横向溢出。 / Reflow across desktop, tablet, and phone widths according to product rules; keep key actions visible, touch targets usable, and the page free of horizontal overflow.
- 无 `backdrop-filter` 时使用实色降级；针对 `prefers-reduced-transparency`、`prefers-contrast: more` 和 `prefers-reduced-motion` 调整覆盖、边界与动态效果。Web CSS 不会自动获得原生系统的完整适配。 / Provide a solid fallback without blur; respond to reduced transparency, increased contrast, and reduced motion. CSS does not inherit the native material's full accessibility behavior.

## 验收 / Verification

检查受影响页面在代表性的桌面、平板和手机宽度下的布局，以及相关交互状态、键盘焦点与取消、浏览器错误、模糊关闭后的可读性。按改动风险运行项目已有检查。分别报告浏览器观察、执行过的测试和未验证项；本地预览不能证明生产效果，部署需单独授权和发布检查。

Inspect affected pages at representative desktop, tablet, and phone widths, including relevant interaction states, keyboard focus and cancel, browser errors, and legibility without blur. Run relevant existing checks in proportion to the change. Report observed browser behavior, executed tests, and unverified items separately. A local preview does not establish production behavior; deployment requires separate authorization and release checks.
