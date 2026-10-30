# 设计风格 · Design Style

一个可按场景推荐、也可自主选择的设计风格库。统一入口是 **`$design-style`**，主要用于海报、PPT与演示文稿，内置 **17种风格**。

告诉Agent“做给谁看、用来做什么、想交付什么”，它就可以推荐合适的视觉方向；已有偏好时，直接指定编号或名称。需要制作成品时，风格规则与当前环境的图片生成、演示文稿或排版工具配合使用。

本仓库还收录了两个完整的网页/UI设计Skill：`liquid-glass-web` 和 `typesafe-inspired-design`。两者的视觉语言已分别整理为统一风格库的第16、17种，原有网页实现规则也保留在仓库中，可独立使用。

## 可以怎么用

**让Agent推荐**

```text
用 $design-style 帮我做一张小学AI课程招生海报。
对象是三到五年级学生和家长，希望有探索感，先推荐一个合适风格。
```

**指定一种风格**

```text
用 $design-style 的第8种山海机关科创风，制作一套课程介绍PPT。
```

```text
用 $design-style 的第16种液态玻璃风做产品介绍海报。
```

```text
用 $design-style 的TypeSafe复古科技风，做一套面向开发者的AI工作流分享PPT。
```

**自己选择，或只要方案**

```text
列出设计风格菜单，我自己选，先不要制作。
```

```text
为教师培训PPT推荐一个风格，只给配色、排版和视觉说明。
```

编号或名称一旦明确，就按用户选择执行。没有指定时，默认推荐一个首选，按需要给少量备选。仅要求推荐时交付推荐；明确要求制作时继续完成相应成品，不额外插入风格确认步骤。

## 17种风格

| 编号 | 风格 | 适用方向 |
| --- | --- | --- |
| 1 | [探索家日志风【经典】](references/01-explorer-journal.md) | 寻宝、成长旅程、探险家手账 |
| 2 | [深网赛博极客风](references/02-cyber-geek.md) | 编程、AI创客、极客技术 |
| 3 | [史诗魔幻策略风【游戏】](references/03-epic-strategy.md) | 团队竞技、积分排位、攻防策略 |
| 4 | [前沿流体玻璃风](references/04-fluid-glass.md) | 数据展示、系统介绍、极光与悬浮几何 |
| 5 | [星际探索学院风](references/05-space-academy.md) | 小学生科幻探索、星球任务与成长路线 |
| 6 | [超级英雄训练营风](references/06-superhero-camp.md) | 勇敢、责任、安全训练与团队协作 |
| 7 | [赛博城市安全局风](references/07-cyber-safety.md) | 较高年级反诈、网络安全、城市侦查 |
| 8 | [山海机关科创风](references/08-shanhai-maker.md) | 国风科创、机关制作、AI灵兽 |
| 9 | [像素冒险闯关风](references/09-pixel-quest.md) | 小学生任务学习、编程闯关、经验奖励 |
| 10 | [未来产品发布会风](references/10-product-keynote.md) | 产品介绍、课程汇报、成果与作品路演 |
| 11 | [儿童AI乐园风](references/11-ai-playland.md) | 低龄、AI与编程启蒙、亲和玩乐 |
| 12 | [机甲工程实验室风](references/12-mecha-lab.md) | 原型制造、代码、测试部署、工程协作 |
| 13 | [梦境发明家工坊风](references/13-dream-workshop.md) | 创意卡、灵感、AI实现想法 |
| 14 | [极地科考安全站风](references/14-polar-station.md) | 科学求证、风险识别与应急决策 |
| 15 | [校园未来研究所风](references/15-campus-institute.md) | 正式进校、开放课、教师培训 |
| 16 | [液态玻璃风【Liquid Glass】](references/16-liquid-glass.md) | 暖杏冷蓝侧光、分层半透明表面、产品与信息展示 |
| 17 | [TypeSafe复古科技风](references/17-typesafe-retro-tech.md) | 大字、暖粉色、方正桌面窗口、真实技术图示 |

第4种偏极光、流体曲线和悬浮展示舞台；第16种偏暖冷侧光、安静的信息层次和玻璃材质。两种可分别选择。第17种保留硬朗的编辑感与技术表达，与暗底霓虹的赛博风有明确区分。

## 安装统一入口

将以下内容放入Agent环境支持的Skill目录下，文件夹名使用 `design-style`：

```text
design-style/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── 17份风格资料
```

Codex默认用户目录为 `~/.codex/skills/design-style/`；Windows对应 `%USERPROFILE%\.codex\skills\design-style\`。如已自定义Skill目录，使用自己的位置。已安装时，更新这三个部分即可。

也可以下载 [设计风格.skill](dist/设计风格.skill)。它是ZIP格式的便携包，解压即可得到上述 `design-style/` 目录，包含统一入口、元数据和17份风格资料，共19个文件。便携包只打包统一入口，两个原始网页Skill在仓库的 `skills/` 目录另行提供。

其他Agent若支持Markdown Skill，可按其加载方式使用；不支持自动发现时，可显式提供 [SKILL.md](SKILL.md) 及所选风格资料。仅做推荐或设计说明不依赖图片生成工具；制作图片、PPT或PDF文件需要环境提供相应能力。

## 给Agent的使用说明

1. 海报或PPT选型时读取根目录 [SKILL.md](SKILL.md)，从索引了解17种候选，再按需读取选中风格的详细资料，不必一次加载全部文件。
2. 尊重用户已经指定的风格；未指定时，综合受众、目标、媒介、信息密度和品牌约束给出推荐。
3. 1–15的资料保留原始风格提示词，16–17是从已有Skill提炼的视觉规则与静态媒介适配。不要将所有装饰都硬塞进一张图。
4. 海报围绕主视觉和行动信息构图；PPT建立封面、章节页和内容页的层级。正文、数据和图表必须清楚可读，长正文不使用装饰性字体。
5. 静态成品中的“呼吸光晕”“漂浮”“故障”等转为柔光、定格构图或局部纹理，只有交付需要且工具支持时才实现动画。
6. 按用户交付要求调用当前环境的制作工具；方案、提示词和实际成品要准确区分。这个风格库本身不提供PPT渲染器，也不保证任意环境均能生成文件。
7. 用户要求液态玻璃或TypeSafe网页/UI实现时，读取对应的完整网页Skill；不要用海报规则替代网页中的响应式、交互与可访问性要求。

## 收录的两个网页Skill

| Skill | 完整规则 | 用途 | 来源版本 |
| --- | --- | --- | --- |
| `liquid-glass-web` | [SKILL.md](skills/liquid-glass-web/SKILL.md) | 以CSS表达液态玻璃材质，保持现有布局、业务行为与响应式约定 | 原版本 `72851acc`；[本仓库收录快照](https://github.com/www228/design-style/blob/616de34c958e73bc51fc390e55f62ed1157c9e97/skills/liquid-glass-web/SKILL.md) |
| `typesafe-inspired-design` | [SKILL.md](skills/typesafe-inspired-design/SKILL.md) | 将TypeSafe启发的大字、暖粉色、硬朗窗口与技术图示用于网站或应用 | 原版本 `cc25adc3`；[本仓库收录快照](https://github.com/www228/design-style/blob/616de34c958e73bc51fc390e55f62ed1157c9e97/skills/typesafe-inspired-design/SKILL.md) |

需要独立调用时，将 `skills/` 内对应文件夹复制到自己的Skill目录，保留其名称和文件结构。已安装同名Skill时，先确认是否需要更新，避免覆盖自己维护的修改。

两个设计Skill现统一在本仓库维护。这里保留原版本的完整 `SKILL.md`、`agents/openai.yaml` 与历史来源标识，快照链接也指向本仓库，使用时无需访问原独立仓库。第16、17种预设对原规则做了海报/PPT适配，相关补充在对应资料中明确标出。

## 仓库结构

```text
.
├── README.md                         # 使用、安装、Agent入口与来源说明
├── SKILL.md                          # 海报/PPT统一选型入口
├── agents/openai.yaml                # “设计风格”的界面元数据
├── references/                       # 17种风格的详细资料
├── skills/
│   ├── liquid-glass-web/             # 完整网页Skill与元数据
│   └── typesafe-inspired-design/      # 完整网页Skill与元数据
└── dist/设计风格.skill                # 统一入口的便携包
```

## 验证范围

仓库更新检查Skill格式、风格编号与本地引用、两个来源Skill的文件一致性，以及便携包内容与统一入口的一致性。具体海报、PPT或网页仍需在实际制作中检查文字、布局、可读性及交付文件；本仓库未提供17套已渲染的成品模板或预览图。
