---
name: vibe-coding-workflow
description: "Standardized person-led + AI-executed product development workflow: project setup (git baseline, environment checklist, tool degradation plan), requirement clarification, spec with completion criteria and a user-runnable acceptance test plan, user-flow → IA → visual mockup with a parameter panel (visual + behavior tokens, export JSON as implementation contract), milestone verification, behavior inventory on redesign, environment handoff, and retrospective. Use when starting a new coding project, planning development with an AI assistant, creating design mockups or parameter-tuning panels, defining acceptance criteria, reviewing build quality, or doing a project retrospective."
version: 1.0.0
---

# vibe coding 工作流

一个人 + AI 协作做产品的标准流程。核心理念：**人管体验，AI 管执行；先定义"完成"再动手；所有"手感"类目标参数化对齐。**

## 贯穿原则

1. 文档纪律：每个项目有唯一事实来源；决策必须回写文档，不靠口头和记忆。
2. 小步单点：每轮只给 1-2 个修改点，验完再发下一个。多目标一锅端必然失望。
3. 人管体验，AI 管执行：用户流程、信息架构、视觉方向由人主导；AI 负责提案、实现与自测。
4. 参数面板驱动手感对齐：视觉参数（色值/字号/间距/圆角/投影）与行为参数（动效时长/缓动/幅度/延迟）都进调参面板，导出参数 JSON 作为实现契约。

## 阶段 0 · 立项（第一天必做）

- [ ] `git init` + 基线提交（防 P0 被原地覆盖）
- [ ] 环境清单：端口 / origin / 服务进程 / 打开的标签页代码代际（避免新旧版本并存误判）
- [ ] 工具降级预案：所用 AI 工具额度/网络/模型不可用时，谁来接手、如何接手
- [ ] 范围决策留痕：被砍清单（能力 / 砍因 / 拾回条件）

## 阶段 1 · 需求

- [ ] 与 AI 一起厘清需求与限制、拆分任务（可借助结构化的 spec 梳理流程）
- [ ] 产出需求文档，**人确认**后才进入下一阶段

## 阶段 2 · 规格与完成标准

- [ ] AI 写 spec + 实施计划文档；**spec 双层语言**：实现细节归 AI，另附产品语言摘要（用户旅程/验收点/不做什么）给人审——审不动的 spec 等于没审
- [ ] 先定义"完成"的标准（写清楚"要验收什么"）：
  - ① 每个任务标注分类：**开发自测 / 用户验收**
  - ② 写一份**用户能照着操作**的验收测试方案
- [ ] **验收方案纳入迭代**：需求变更 → 同步更新验收方案

## 阶段 3 · 设计

- [ ] 基于**用户使用流程**（主流程、分支流程 1、分支流程 2……）提出页面清单，与人对齐
- [ ] 形成**信息架构（IA）文档**，人确认
- [ ] 出视觉稿：使用模板 `assets/mockup-template.html`——
  - 复制模板到项目，**把设计令牌替换成项目自己的风格**（色值/字体/质感）；模板默认值是占位符，不得当成品风格用
  - 帧式结构：每帧一个页面（手机壳或桌面画布），标注帧号与说明
  - 调参面板：视觉参数 + 行为参数（时长/缓动/幅度/延迟），尽量全面
  - 人调参满意后「导出参数」JSON → 作为实现依据（实现方照参数表落地，不自由发挥）
- [ ] 动效/交互必须有行为规格：静态帧承载不了行为，帧图上的文字承诺（如"落进……筐"）必须显式登记

## 阶段 4 · 开发

- [ ] 按任务书小步推进（每轮 1-2 修改点）
- [ ] 每完成一个里程碑：截图 + 日志留痕
- [ ] 跨切面契约显式化：层级体系（z-index 图谱）、页面状态机等写成文档；修改后**回归受影响场景**（修局部必验全局）
- [ ] **文案集中管理**：可见文案抽到独立配置文件（如 copy.js），静态用 data-copy 绑定、动态读配置对象；改文案只动配置不碰逻辑；改后同步升缓存参数（避免浏览器旧脚本假阴性）

## 阶段 5 · 验收（含主观项与真机）

- [ ] **行为清点**（改版必做）：上一版每个行为（动效/交互/状态变化）逐条对照新版帧图，标 **保留 / 变更 / 删除**，删除要有理由
- [ ] 验收测试方案逐条执行；**主观项给具体观察点**（如"掉进筐里弹两下看着爽吗"→ 观察：落点、弹跳次数、节奏、是否想反复扔）
- [ ] 真机走查：真实设备、真实用户旅程（浏览器自动化回归 ≠ 真机体验）
- [ ] 设计稿改版 → 验收项重新校验（真实联动，不是文档里出现就算）

## 阶段 6 · 交接

- [ ] HANDOFF 文档：当前状态 + 环境清单（端口/origin/标签页代际/服务状态）+ 下一步
- [ ] 工具降级预案触发时，按预案交接给备用执行方

## 反例信号（看到就停下）

- "AI 应该能理解我的想法" → 先拆需求、先对齐，再动手
- "一次对话把所有问题都解决" → 拆成单点，逐批验证
- "新模型更强，应该能一次理顺烂摊子" → 模型能力 ≠ 替代清晰规格，先拆问题再换工具
- "设计稿上有这句话，应该就会实现" → 没进行为规格/验收清单 = 未承诺
- "验收方案是开始写的那版" → 需求变了方案没变 = 流程漏洞
- "修复了一个 bug，应该不会影响别的" → 跨切面契约没查，回归没跑
- "环境里有旧的东西，应该没关系" → 旧标签页/旧进程/旧数据会制造误判
- "发布目录里的文件是旧的，以为发的是最新代码" → 发布前校验发布目录（版本标记/时间戳），发布后探测公网 URL 确认内容，"验过才算完"同样适用于部署

## 资源

- 视觉稿模板（参数化框架，中性风格）：[assets/mockup-template.html](assets/mockup-template.html)
- 实战案例：空瓶控项目复盘（2026-08-20）——此流程的全部条目来自该案例的真实踩坑
