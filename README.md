<div align="center">

# awesome-dsh

**DeepSeek Harness（DSH）中文精选生态指南**

按「你想干什么」组织的插件 / 工具 / 资源清单 · 人工筛选 · 附一句话点评与安装入口

[DSH 官方仓库](https://github.com/deepseek-ai/deepseek-harness) · [提交收录](CONTRIBUTING.md) · 更新日志见文末

</div>

---

> **什么是 DSH？** DeepSeek Harness 是 DeepSeek 开源的 Agent 运行框架（MIT 协议，2026-08-13 发布）。
> 官方公式：**模型 + Harness = Agent**。模型负责推理，Harness 负责把模型接到文件系统、终端、沙箱和工具上，并组织整个任务循环。
> 它不是模型，也不是成品应用，而是「一切皆插件」的 Agent 底座——模型、工具、会话、沙箱、Agent 循环、UI 全部可替换。
>
> ⚠️ DSH 目前为 v0.1 开发者预览版，官方明确会有破坏性变更，暂不建议直接用于生产环境。

## 快速上手

```bash
# 方式一：npm 直接启动（装好 Node.js 后一行命令）
npx @deepseek-ai/dsh web
# 打开 http://127.0.0.1:3080，填入 API Key 即可

# 方式二：从源码运行
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
pnpm dsh web
```

默认支持近 40 个模型（DeepSeek / OpenAI / Anthropic / Google / Kimi 等），BYOK 模式，自带 API Key 即用。

## 三个必须先搞懂的概念

| 概念 | 是什么 | 一句话 |
|---|---|---|
| **Plugin 插件** | Cordis 运行时模块（代码），注册新能力到 `ctx.tools` / `ctx.llm` / `ctx.fs` 等 | 改变 Agent **能做什么**（装硬件） |
| **Skill 技能** | Markdown 定义的过程性知识，注入提示词 | 改变 Agent **怎么做**（发手册），兼容 Claude Code skills |
| **Preset 预设** | 插件组合 + 运行规则的打包，四种官方模式本质都是 preset | 决定 Agent **带着什么工具箱上场** |

四种官方模式：**Standard**（完整编程 Agent，对标 Claude Code/Codex）/ **PTC**（模型写代码串联工具调用，中间数据不进上下文，省 token）/ **Minimal**（仅 bash + 文件编辑器）/ **Creation**（创建你自己的 preset）。

---

## 🧭 官方资源

- [deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) — 官方主仓库，MIT 协议
- [架构文档 docs/architecture.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md) — 扩展点、事件系统、seam 机制，二开必读
- [Cordis 论文：A Programming Paradigm for Spatiotemporal Composability](https://github.com/cordiverse/paper) — 北大 & DeepSeek 联合论文，底层插件系统的理论基础
- [GitHub Discussions](https://github.com/deepseek-ai/deepseek-harness/discussions) — 反馈与讨论
- [官方 Discord](https://discord.gg/Ycq5dCaS4) — 社区
- [dsh-plugin 话题](https://github.com/topics/dsh-plugin) — 全量插件池（1000+ 仓库，本清单从这里人工筛选）

## 📚 精选索引与手册（先看这些）

- [dsh-handbook](https://github.com/Electricitysheep/dsh-handbook) — 从 0 到 1 的 DSH 深度手册，含插件开发教程
- [awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin) — 中英双语插件精选列表
- [awesome-dsh-plugins](https://github.com/AdamPlatin123/awesome-dsh-plugins) — 自动扫描全量索引（雷达），找冷门插件用
- [awesome-deepseek-harness](https://github.com/0xsline/awesome-deepseek-harness) — 英文生态精选，带安装命令

## 🖥️ 想要更好的界面和工作台

- [dsh-web-ui](https://github.com/zhu1090093659/dsh-web-ui) ⭐1.7k — Web UI 增强全家桶：任务看板、Git 图谱、右侧面板、手机远程界面、实时 token 统计、皮肤中心，一个包补齐官方界面的缺项
- [DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar) — 把侧边栏升级成 VS Code 式工作台：文件管理、代码编辑、真实终端、Git、Diff、内嵌浏览器、子代理状态
- [dsh-TUI](https://github.com/ccch1mneyyy/dsh-TUI) ⭐792 — Claude Code 风格全屏终端 TUI，像素鲸鱼顶栏、流式思考、双击 Esc 时间回溯、上下文进度条，官方公众号收录
- [deepseek-harness-desktop](https://github.com/anywhere-labs/deepseek-harness-desktop) — 现代化桌面端封装
- [deeptide](https://github.com/paean-ai/deeptide) ⭐1k — Swift 原生 macOS 客户端，原生党福音
- [dsh-at-file](https://github.com/omdsh-dev/dsh-at-file) — 输入框直接 `@` 引用文件，小而刚需
- [dsh-genui](https://github.com/omdsh-dev/dsh-genui) — 让模型在回复里直接渲染图表、表格、表单、Diff、Mermaid、交互面板

## 👁️ 想让纯文本模型「看得见」

- [modlens](https://github.com/liustack/modlens) ⭐1.2k — 全网第一个 DSH 视觉插件，粘贴图片即得结构化 JSON（OCR、版面、语义），给 DeepSeek 纯文本模型外挂视觉通道
- [agent-vision-toolkit](https://github.com/Anionex/agent-vision-toolkit) ⭐800 — 视觉工具箱：多图理解、图片问答、前端 UI 还原、GUI 自动化

## ⚙️ 想做自动化和批处理

- [dsh-automation](https://github.com/titanwings/dsh-automation) — 给 DSH 补上自动化编排能力，配合 PTC 模式食用更佳
- [coding-tools-mcp](https://github.com/xyTom/coding-tools-mcp) — 通过 MCP 给任意 Agent 赋予编码能力

## 🧠 想要更聪明的 Agent

- [colleague-skill](https://github.com/titanwings/colleague-skill) ⭐21.9k — 「数字生命」知识蒸馏与技能生成，把经验沉淀为可复用 skill
- [Vibe-Skills](https://github.com/foryourhealth111-pixel/Vibe-Skills) — 本地 skills 自动路由 + 工作流智能编排
- [archify](https://github.com/tt-a1i/archify) ⭐12.4k — 生成可验证的架构图 / 工作流图 / 时序图 / 数据流图，自包含 HTML

## 🌐 生态平台与工作空间

- [open-design](https://github.com/nexu-io/open-design) ⭐86.1k — 开源 Claude Design 替代方案，把编码 Agent 变成设计引擎，支持 20+ CLI
- [iPolloWork](https://github.com/Devin-AXIS/iPolloWork) — 下一代 AI 工作空间，集成 DSH 做子代理委派
- [mobius](https://github.com/nutshellai-tech/mobius) — 自进化开源 Agent OS
- [OpenBiliClaw](https://github.com/whiteguo233/OpenBiliClaw) — 本地自进化内容发现 Agent，支持 B站 / 小红书 / 抖音 / YouTube / X / 知乎 / 微博

## 🐳 趣味生态（DSH 社区特色）

> 别小看这个分类——桌宠、皮肤、小游戏泛滥，说明生态活性极高，和当年 VSCode 皮肤潮一个信号。

- [dsh-ui-whale](https://github.com/omdsh-dev/dsh-ui-whale) — 会话标题栏养像素鲸鱼，空闲眨眼、思考时游动、回合结束喷水
- [dsh-deep-whale](https://github.com/Small-tailqwq/dsh-deep-whale) ⭐237 — 鲸鱼娘皮肤系列
- [petdex](https://github.com/crafter-station/petdex) — 动画宠物画廊，跨 Codex / Claude Code / DSH 等多 Agent
- [dsh-minigames](https://github.com/lhh010/dsh-minigames) — 侧边栏 18 款摸鱼小游戏
- [dsh-ads](https://github.com/Nagi-ovo/dsh-ads) — 给 Web 界面加 2005 年中文网站风格侧栏广告（行为艺术，旁边甚至长出了一个专门屏蔽它的插件）

---

## 📖 中文学习资源

- [DeepSeek 把 Harness 开源了：模型、工具、Agent Loop 全是插件 — InfoQ](https://www.toutiao.com/article/7673585430633120291) — 架构层面讲得最透的一篇
- [DeepSeek Harness 拆解：一套能拼装的 Agent 架构 — 腾讯新闻](https://new.qq.com/rain/a/20260814A0B3W500) — 含插件生态盘点
- [从 0 到 1 带你速通 DeepSeek Harness — 搜狐](https://www.sohu.com/a/1062621298_121675819) — 上手向，带插件实测截图
- [DeepSeek 开源 Harness：一切皆插件 — 阿里云开发者社区](https://developer.aliyun.com/article/1755877) — 插件生态速览
- [DeepSeek Harness Hands-On: Four Work Modes — Pandaily](https://www.pandaily.com/deepseek-harness-hands-on-four-modes-model-plus-harness-equals-agent-aug2026) — 英文，四种模式实测
- [Everything is a Plugin — NYU Shanghai RITS](https://rits.shanghai.nyu.edu/ai/deepseek-harness-cordis-everything-is-a-plugin) — 英文，Cordis 技术细节最深

## 🔌 如何安装插件

通用机制（具体以各插件仓库 README 为准，部分提供 `install.sh`）：

```bash
# 安装 DSH CLI（已装可跳过）
npm install -g @deepseek-ai/dsh

# 把插件装入指定 profile
dsh plugin --profile <profile名> add <插件包名>

# 用该 profile 启动
dsh --profile <profile名>
```

插件纯挂载、零核心改动，卸载即回滚。Windows 用户注意：目前部分沙箱后端缺失，会退回完全访问模式，敏感环境请先检查 profile 配置。

## 📤 如何发布你自己的插件

1. 按 Cordis 插件规范开发（参考 [架构文档](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md) 与 [扩展指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cookbook/extension-cookbook.md)）
2. 仓库打上 `dsh-plugin` topic，即可被社区发现
3. 官方目前不接受外部 PR，但**官方插件与社区插件地位同等**
4. 欢迎向本清单提交收录（见 [CONTRIBUTING.md](CONTRIBUTING.md)）

---

## 收录标准

1. **能用**：仓库可访问、安装方式明确，优先收录实测可用项
2. **有用或有趣**：解决真实问题，或体现生态活性
3. **人工筛选**：不做全量索引（全量请看 [awesome-dsh-plugins](https://github.com/AdamPlatin123/awesome-dsh-plugins) 雷达）
4. Star 数为 2026-08-14 快照，仅供参考

## 更新日志

- **2026-08-14** 首版：官方资源 / 界面工作台 / 视觉 / 自动化 / Agent 增强 / 生态平台 / 趣味生态 / 中文学习资源，收录 30+ 条目

## License

[MIT](LICENSE)
