# Jasmine Time 索引地图

个人工程资产库。用途：**打开本稿 → 按意图跳到目录/文件**，不要在整仓里盲搜。

分类口径：

| 目录 | 放什么 | 不放什么 |
|------|--------|----------|
| `Trellis/` | 可安装到新仓库的 **你的** Trellis 包 | 上游完整源码 |
| `trellis_origin/` | [mindfold-ai/Trellis](https://github.com/mindfold-ai/Trellis) 整仓 | 日常安装入口 |
| `Awesome skill example/` | Skill 写法样例 | 可独立跑的完整产品 |
| `Awesome MCP/` | MCP Server 样例 | 浏览器 Host 产品 |
| `Awesome Coding Tool/` | 编码期工具（图、SDD、循环、CLI） | Skill 教程本体 |
| `Awesome Application/` | 完整应用 / Agent Runtime | 单点 MCP |
| `Awesome Design/` | 视觉 / DESIGN.md / UI 模板 | 后端产品 |
| `Awesome Plugin/` | 可独立运行的产品/插件包 | 规范笔记 |
| `Awesome Thought/` | 设计取舍笔记 | 可运行代码 |
| `Agent Test/` | 验证协议（人/Agent 可读） | 可执行 skill 本体 |
| `Awesome website/` | 在线工具书签 | 克隆下来的站点 |
| `Git 规范/` | 基础设施心智模型 | Git 命令手册 |

配套：根 [`README.md`](./README.md) 是简介；本稿是 **定位图**。

---

## 0. 按意图跳转

| 我想… | 去 |
|--------|----|
| 给新仓库装 Trellis | [`Trellis/install.ps1`](./Trellis/install.ps1) · [`Trellis/README.md`](./Trellis/README.md) |
| 改官方 Trellis（explore / preflight / CLI） | [`trellis_origin/README_NEW.md`](./trellis_origin/README_NEW.md) · [`trellis_origin/packages/cli/`](./trellis_origin/packages/cli/) |
| 写一个新 Skill | [`Awesome skill example/README.md`](./Awesome%20skill%20example/README.md) |
| 把技术方案讲给非专家听（保留术语） | [`Awesome skill example/architecture-explainer`](./Awesome%20skill%20example/architecture-explainer/) |
| 压缩 agent 上下文/输出、省 token | [`Awesome skill example/caveman`](./Awesome%20skill%20example/caveman/) |
| 看多平台 harness 大 skill 包怎么组织 | [`Awesome skill example/ECC`](./Awesome%20skill%20example/ECC/) |
| 写一个新 MCP | [`Awesome MCP/README.md`](./Awesome%20MCP/README.md) |
| Agent 环境依赖查缺补漏 | `trellis_origin` 的 `trellis-preflight` · [§2.0](./trellis_origin/README_NEW.md) |
| 建 spec 代码地图（新项目从零 / 已有项目反推） | 参考实现：[`trellis_origin/.trellis/spec/`](./trellis_origin/.trellis/spec/)；技能 `trellis-spec-bootstrap`（反推）· `trellis-update-spec`（增量） |
| 代码图 / 定位符号 | 仓收藏：`codegraph` / `code-graph-rag`；**Trellis explore 不用图**，读 `spec/index.md` + Grep |
| Spec 驱动开发（非 Trellis） | `Awesome Coding Tool/spec-kit` 或 `OpenSpec` |
| PRD 拆 user story 后让 Claude/Amp 循环跑到全绿 | [`Awesome Coding Tool/ralph`](./Awesome%20Coding%20Tool/ralph/) |
| 验证「做没做对」而不是「测过没」 | [`Agent Test/`](./Agent%20Test/) + `requirement-driven-verification` |
| 让页面长得像某品牌 | [`Awesome Design/README.md`](./Awesome%20Design/README.md) |
| 选色板/字体/产品类型 | `Awesome Design/ui-ux-pro-max` |
| 浏览器给 Agent 用 | `chrome-devtools-mcp` / `agent-browser` / `gpt-project` |
| 把已有软件变成 Agent 能调的 CLI | [`Awesome Application/CLI-Anything`](./Awesome%20Application/CLI-Anything/) |
| 多个 coding agent 共用一个可分离/重连的终端 runtime | [`Awesome Application/herdr`](./Awesome%20Application/herdr/) |
| 插件化 Agent Harness（DeepSeek，一切皆插件） | [`Awesome Application/deepseek-harness`](./Awesome%20Application/deepseek-harness/) |
| 本机硬件能跑哪个本地模型 | [`Awesome Application/llmfit`](./Awesome%20Application/llmfit/) |
| AI 渗透测试 / 漏洞验证（仅授权目标） | [`Awesome Application/strix`](./Awesome%20Application/strix/) |
| Agent 用已有数据库连接查表/跑 SQL（MCP） | [`Awesome Application/dbx`](./Awesome%20Application/dbx/) |
| PDF/Office/扫描件 → 结构化文档给 RAG | [`Awesome Application/docling`](./Awesome%20Application/docling/) |
| 多格式文件 → Markdown 给 LLM 管道 | [`Awesome Application/markitdown`](./Awesome%20Application/markitdown/) |
| 本机 Windows Python/Git Bash 坑 | [`本地环境问题.md`](./本地环境问题.md) |

---

## 1. 工作流内核

### `Trellis/` — 可迁移安装包（日常入口）

把任务流、skills、commands、agents 装进任意目标仓。产品知识仍写在目标项目的 `.trellis/spec/`。

| 产物 | 作用 |
|------|------|
| `install.ps1` | 安装入口：`-Target` + 可选 `-Modes` |
| `modes.yaml` / `VERSION` / `MANIFEST.md` | 装哪些层、版本 |
| `kit/` | 默认拷进目标仓：`.trellis`、`.agents/skills`、`.cursor`、`.claude`、OpenSpec、templates |
| `kit/.trellis/` | workflow、scripts、spec stub、tasks |
| `modes/meta-router/` | L2：多仓根只做指针 |
| `modes/closedloop/` | L3：Driver / Orchestra / 证据账本 |
| `docs/architecture.md` · `docs/migrate.md` | 结构与迁移 |

```powershell
cd D:\Projects\Jasmine-Time\Trellis
.\install.ps1 -Target D:\Projects\my-new-app
```

### `trellis_origin/` — 上游完整仓库（改官方行为来这里）

对照：`Trellis/` = 你的可安装产物；`trellis_origin/` = 官方 CLI + 技能模板 + 轻量主线文档。

| 产物 | 作用 |
|------|------|
| `README_NEW.md` | **轻量主线说明**（explore / preflight / 三条路径）— 改设计先读这个 |
| `README.md` | 上游对外 README |
| `packages/cli/` | CLI、平台 configurator、 **skill/script 模板真相源** |
| `packages/core/` | `@mindfoldhq/trellis-core` |
| `.trellis/spec/` | **spec 代码地图的参考实现**：根 `index.md` 扁平路由直达叶子；层 `index.md`（`cli/backend/` 等）只服务 before-dev，不进 explore 路由 |
| `.trellis/scripts/preflight.py` | 环境探针（与 `packages/cli/src/templates/trellis/scripts/preflight.py` 字节一致） |
| `.trellis/scripts/task.py` · `get_context.py` | Task lane 机器面 |
| `.agents/skills/trellis-*` 及 `.cursor/.claude/.opencode/.omp/.pi` | 各平台 skill 狗粮；改 skill 后要同步 |
| `TRELLIS_LIGHTWEIGHT_SKILLS_REVIEW.md` | 轻量化设计取舍长文 |
| `docs-site/` · `marketplace/` | 文档站与市场（submodule） |

环境就绪：`python3 ./.trellis/scripts/preflight.py --json`（技能 `trellis-preflight` 会按报告查缺补漏）。

---

## 2. Awesome skill example — Skill 怎么写

开发参考：[`Awesome skill example/README.md`](./Awesome%20skill%20example/README.md)

| 项目 | 作用 | 先打开 |
|------|------|--------|
| `brainstorming` | 流程门禁型：创意前先设计、禁止跳步写代码 | `SKILL.md` · `visual-companion.md` |
| `requirement-driven-verification` | 需求驱动三层验证（Trellis task / PRD → 证据 → Verdict） | `README.md` · `SKILL.md` · `scripts/` |
| `frontend-integrity` | 前端完整性清单 + CLI；Live Playwright 在 `test-worker/` | `README.md` · `SKILL.md` · `adapters/` |
| `OpenSpec` | Fission-AI 规格流：propose / apply / archive | `skills/openspec-*/SKILL.md` · `SOURCE.md` |
| `superpowers` | obra/superpowers 完整方法论 skill 包 | `README.md` · `.agents/skills/` |
| `ECC` | 多平台 agent harness「操作系统」：285+ skills、agents、hooks、memory/instincts、AgentShield；Claude/Codex/Cursor/OpenCode 等 | `README.zh-CN.md` · `.agents/skills/` · `skills/` · `install.sh` · `the-shortform-guide.md` |
| `skills`（mattpocock） | 可组合的小 skill，反对被 GSD/BMAD 夺走控制权 | `README.md` · 各 `SKILL.md` |
| `Tech-Doc-Style-Chinese` | 中文技术/产品文案克制规范 | `SKILL.md` · `references/` |
| `architecture-explainer` | 讲解/教学：把 plan/架构/code-review 讲懂；保留英文术语；ASCII 图；取舍与过度设计；「这个方案怎么样」切 Review | `SKILL.md` · `README.md` |
| `caveman` | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)：让 agent **少说也少读**；wrap 30+ agent、proxy、可选 MCP shrink；benchmark 约 -33% provider input tokens | `README.md` · `INSTALL.md` · `docs/WRAP-BENCHMARK.md` · `docs/README.md` |

> `ui-ux-pro-max` 实体在 [`Awesome Design/ui-ux-pro-max`](./Awesome%20Design/ui-ux-pro-max/)，不在本目录。

`ECC` 先读 `README.zh-CN.md` 或 `the-shortform-guide.md`。Claude Code：`/plugin marketplace add https://github.com/affaan-m/ECC` → `/plugin install ecc@ecc`。**勿叠装**（plugin + 全量 manual 会重复 hooks/skills）。与 Trellis 轻量主线并存时，ECC 是参考库/可选 overlay，不替代 Task lane 的 RDV 门。

`caveman` 先读 `README.md` 或 `INSTALL.md`；一键装：`irm …/install.ps1 | iex`（Windows）或 `curl …/install.sh | bash`。与 Trellis 轻量主线：**可选 overlay**，会改 hooks/statusline/输出风格；不要与 ECC 整包叠装前不评估重复注入。

---

## 3. Awesome MCP — MCP 怎么接

开发参考：[`Awesome MCP/README.md`](./Awesome%20MCP/README.md)

| 项目 | 作用 | 关键产物 |
|------|------|----------|
| `chrome-devtools-mcp` | 官方：Agent 控真实 Chrome（截图/网络/性能） | `src/` · `docs/` · `skills/` |
| `github-mcp-server` | 官方 GitHub：Issues/PR/仓库（远程 URL 或本地） | `README.md` · `docs/` |
| `gpt-project` | CDP 桥：用已登录 Chrome 问 ChatGPT，无 API Key | `src/` · `scripts/` · 口令 9222 |
| `plan-review-mcp` | Plan/PRD 只读审核（Claude / Codex / Pi / ensemble） | `src/` · `scripts/run-mcp.mjs` |
| `agent-browser` | Vercel：Rust CLI 浏览器自动化（可当技能/CLI，不单是 MCP） | `cli/` · `skills/` · `packages/` |

Cursor 接入骨架见该目录 README。

---

## 4. Awesome Coding Tool — 编码期基础设施

| 项目 | 作用 | 关键产物 |
|------|------|----------|
| `codegraph` | 本地代码知识图 MCP（本仓 `codegraph_explore` 用的就是这类） | `src/` · `docs/` · `install.ps1` |
| `code-graph-rag` | Tree-sitter → Memgraph 图；自然语言改/查代码 | `README.md` · `.cgr/` 运行时数据（若有） |
| `code-review-graph` | 给 code review 预建结构图，少让模型重读整仓 | `README.md` · `install`/`build` CLI |
| `diagram-design` | 编辑级架构图 skill（27 种视觉类型） | `SKILL.md` · `docs/screenshots/` |
| `spec-kit` | GitHub Specify：Spec-Driven Development CLI（**编码工具，不是 skill 包**） | `README.md` · `presets/` · `extensions/` · `examples/bundles/` |
| `OpenCLI` | 网站/已登录 Chrome → 确定性 CLI；也可 Browser Use | `README.md` · `README.zh-CN.md` · 内置站点 adapter |
| `loopx` | 长跑 Agent 的本地控制面（可复盘、可重启） | `README.md` · 官方 docs 站点链接 |
| `ralph` | PRD → `prd.json` → `ralph.sh` 循环：每轮新 Claude/Amp 实例，只做一个 user story；记忆靠 git + `progress.txt` + `prd.json` | `README.md` · `ralph.sh` · `prd.json.example` · `skills/prd/` · `skills/ralph/` · `prompt.md` / `CLAUDE.md` |
| `Switchyard` | Rust LLM 代理：协议翻译 + 多后端路由（给 Claude/Codex 指开源模型） | `crates/` · `examples/` · `benchmark/` |
| `obsidian-skills` | Obsidian 知识库 Agent Skills | `README.md` · 各 skill |

选型：要「当前文件/符号」用 `codegraph`；要 Memgraph 调用链用 `code-graph-rag`（重，preflight 不自动拉起）。**`trellis-explore` 不用二者**：先读 `.trellis/spec/index.md`，再用 Grep。

`ralph` 先读 `README.md`：用 `skills/prd` 写 PRD → `skills/ralph` 转 `prd.json` → 拷 `ralph.sh` 到目标仓 `scripts/ralph/` 跑；依赖 `jq` + git；Claude 用 `--tool claude`。也可 `/plugin marketplace add snarktank/ralph` 装 skill 包。**与 Trellis 轻量主线**：只用其 skills 做 story 切片进 `implement.md`；自治 `ralph.sh` 放独立 loop-lab，不替代 Task lane 的 approve / RDV / archive。

---

## 5. Awesome Application — 完整产品 / Runtime

| 项目 | 作用 | 关键产物 |
|------|------|----------|
| `agency-agents` | 角色化专家 Agent 花名册（可装进各 IDE） | `README.md` · 各 agent 定义 |
| `claude-video` | `/watch`：让 Claude 看视频（yt-dlp/ffmpeg/字幕） | skill / plugin 安装说明 |
| `CLI-Anything` | 让任意软件变成 Agent 可调 CLI（Pi/Cursor/Claude 等）。Hub：`pip install cli-anything-hub` → `cli-hub install <name>` | `README.md`/`README_CN.md` · `cli-hub/` · `cli-anything-plugin/`（7 阶段生成器）· `<app>/agent-harness/`（约 70+ 个，如 blender/gimp/freecad）· `cli-hub-meta-skill/SKILL.md` · `registry.json` |
| `corsair` | 统一集成层：MCP 接上后 Agent 用各 SaaS，密钥不进对话 | `packages/corsair` · `packages/<vendor>/` · `demo/` · `explorer/` |
| `DeepTutor` | 终身个性化辅导（Python + Next.js） | `README.md` · CLI |
| `deepseek-harness` | DeepSeek 开源 Agent Harness（`dsh`）：**一切皆插件**（Cordis）。开发者预览，会破兼容。Web UI：`npx @deepseek-ai/dsh web`（默认 `:3080`） | `README.zh.md` · `AGENTS.md` · `docs/` · `packages/`（core/llm/skill/web…）· `vendor/`（Cordis）· `python/` · `website/` |
| `dspy` | 用 Python 编程 LM，而不是手写脆 prompt | `README.md` · docs: dspy.ai |
| `firecrawl` | 网页抓取/搜索 → Markdown/结构化，给 Agent 当网页上下文 | `README.md` · API |
| `herdr` | coding agent 终端 runtime：后台常驻、pane 标 working/blocked/idle、关盖/断网会话还在。不替换 Claude/Codex/Cursor，只托管它们的终端。Rust 单二进制；Windows 有 `install.ps1` | `README.zh-CN.md` · `AGENTS.md` · `skills/herdr/SKILL.md` · `src/` · `website/install.ps1` |
| `llmfit` | 按本机 RAM/CPU/GPU 给本地模型打分（fit/speed/quality/context）；TUI 默认，也有 JSON CLI。对接 Ollama / llama.cpp / MLX / LM Studio | `README.zh.md` · `AGENTS.md` · `docs/`（tui/cli/providers/benchmarking）· `llmfit-tui/` · `llmfit-core/` · `data/` · `skills/` |
| `pi` | Pi Agent Harness：coding-agent / agent-core / 多厂商 LLM | `packages/coding-agent` · `packages/agent` · `packages/ai` · `packages/tui` |
| `pi-gui` | Pi 的桌面壳（时间线、worktree、diff）；**不是另一套 runtime** | `README.md` · `docs/assets/` |
| `prime-agent` | 自改进 RLM Agent（IPython 控制面 + 持续 harness 状态） | `README.md` |
| `Proma` | 本地优先桌面：Chat + Agent + Skills + MCP + 记忆（`~/.proma/`） | `README.md` · `tutorial/` · `proma-thinking/` |
| `ragflow` | 开源 RAG + Agent 上下文引擎 | `README.md` · `api/` · `web/` · `docker/` · `agent/` |
| `strix` | 开源 AI 渗透测试：多 Agent 动态跑真实 PoC、给补丁与报告。本机 CLI 要 Docker + LLM Key；也可用 managed `app.strix.ai`。**只测有书面授权的目标。** | `AGENTS.md` · `skills/`（4 个 SKILL）· `strix/`（agents/tools/runtime）· `containers/` · `docs/` · 结果目录 `strix_runs/` |
| `dbx` | [t8y2/dbx](https://github.com/t8y2/dbx)：Rust 轻量跨平台数据库客户端（~20 MB、80+ 库）。桌面 / Docker Web / CLI；内置 AI 写 SQL；**MCP Server**（`@dbx-app/mcp-server`）让 Cursor/Claude 复用 DBX 里已有连接查库 | `README.zh-CN.md` · `packages/mcp-server/README.md` · `deploy/dockerhub/README.md` · 站点 [dbxio.com](https://dbxio.com) |
| `docling` | IBM/LF 文档解析：PDF/Office/HTML/音频等 → Markdown/JSON，布局/表格/公式感知，给 RAG 与 Agent 当输入 | `README.md` · `packages/docling/` · docs: docling-project.github.io |
| `markitdown` | Microsoft AutoGen 团队：PDF/PPT/Word/Excel/图片/音频/YouTube 等 → Markdown，轻量给 LLM 文本管道；含 MCP 包 | `README.md` · `packages/markitdown/` · `packages/markitdown-mcp/` |
| `Anthropic-Cybersecurity-Skills` | 817 个网络安全 Agent Skills（29 域）；MITRE ATT&CK / NIST CSF / OWASP 映射；蓝队/合规/授权渗透场景参考库 | `README.md` · `skills/` · `mappings/` · `tools/` |

`corsair` 子包极多（Gmail、Slack、Notion…）：先读 `packages/corsair`，再进具体 vendor 包。

`CLI-Anything` 用现成 harness 走 Hub；造新 CLI 走 `cli-anything-plugin`。站点：[clianything.cc](https://clianything.cc/)。

`llmfit` 先读 `README.zh.md` 或 `AGENTS.md`；Windows：`scoop install llmfit`。测真实 tok/s 看 `docs/benchmarking.md`。

`herdr` 先读 `README.zh-CN.md` 或 `AGENTS.md`。Windows 测试版：仓库内 `website/install.ps1`，或上游 `irm https://herdr.dev/install.ps1 | iex`。Skill 只在 `HERDR_ENV=1`（跑在 herdr pane 里）时生效。站点：[herdr.dev](https://herdr.dev/)。

`deepseek-harness` 先读 `README.zh.md` 或 `AGENTS.md`；改 `packages/` 先读 `docs/architecture.md`。站点：[deepseek.com/harness](https://deepseek.com/harness)。

`strix` 先读 `AGENTS.md`；给 Cursor/Claude 装 skill：`npx skills add usestrix/strix`（本仓已有源码副本 `skills/`）。

`dbx` 先读 `README.zh-CN.md`；Windows：`scoop bucket add dbx https://github.com/t8y2/scoop-bucket` → `scoop install dbx`。MCP：`npm i -g @dbx-app/mcp-server`，配置见 `packages/mcp-server/README.md`。Docker：`t8y2/dbx:latest`，默认端口 `4224`。

---

## 6. Awesome Design — 长什么样

[`Awesome Design/README.md`](./Awesome%20Design/README.md) 有产品大类 → 首选品牌表。

| 项目 | 作用 | 关键产物 |
|------|------|----------|
| `awesome-design-md` | 上游 VoltAgent：把 `DESIGN.md` 丢进项目让 Agent 跟视觉 | `design-md/<brand>/DESIGN.md` · `preview.html` |
| `ui-ux-pro-max` | 设计智能：风格/色板/字体检索（知识库 + `scripts/`） | `SKILL.md` · `data/` · `scripts/search.py` |
| `impeccable` | 前端设计 skill + 23 命令 + 确定性 detector | `README.md`（`npx impeccable install`） |
| `ai-website-cloner-template` | 给定 URL，Agent 反解成 Next.js | `/clone-website` · `docs/` |
| `shadcn-admin` | shadcn + Vite 管理后台 UI 参考（非 starter） | `public/images/` · 各 page |

和其它资产的分工：**本目录 = 长得像谁**；`ui-ux-pro-max` = 怎么选；`Awesome Plugin` = 可跑的成品。

---

## 7. Awesome Plugin — 可独立跑的包

| 项目 / 文件 | 作用 | 关键产物 |
|-------------|------|----------|
| `indonesia-intel` | 中国→印尼情报 ingest MVP（FastAPI + Ops 看板 + MCP） | `app/` · `web/` · `mcp_server/` · `jobs/` · `.env.example` |
| `agent-plugins.md` | Vercel Agent Plugins 1.0 笔记：Skills+MCP 打成 `plugin.json` 包 | 规范对照表 |

看板：`http://127.0.0.1:8765/app/#feed`（见该 README）。

---

## 8. Agent Test — 验证协议（不是测试代码仓）

可执行实现在 skill：[`requirement-driven-verification`](./Awesome%20skill%20example/requirement-driven-verification/)。

| 文件 | 作用 |
|------|------|
| `prd-driven-verification-loop.md` | **为什么** Test > 写代码、反自测假绿 |
| `three-layer-verification.md` | **主协议**：L1 代码/测试可信 · L2 符合 PRD · L3 用户任务完成 |
| `PRD.md` | 验证 skill 自己的设计 PRD |
| `verification-cheat-sheet.md` | Paperclip 场景命令速查 |

宣称完成必须有 Verification Verdict + Evidence Header（见三层协议）。

---

## 9. Awesome Thought — 取舍笔记

| 文件 | 一句话 |
|------|--------|
| `4-强模型与过度脚手架-Superpowers.md` | 流程太细会从增强模型变成替模型决策 |
| `5-桌面应用去WebView化-Electron-Tauri-GPUI.md` | 「全员 GPUI」方向对、结论过满 |
| `6-Agent-Runtime-Prompt-Cache-Prefix稳定性.md` | cache 差距 ≈ Prompt 前缀稳不稳 |
| `7-Go与Agent-Verifiability-机器验证优于Vibe.md` | Go 的优势是写完更好验证，不是更好写 |

### `Git 规范/`

| 文件 | 作用 |
|------|------|
| `AI应用工程-基础设施心智模型.md` | Git → CI → 镜像 → 容器 这一层「出了问题往哪找」 |

### `Awesome website/`

| 文件 | 作用 |
|------|------|
| `目录.md` | 书签：`namethatui`（视觉词典→prompt）、`reicon`（图标 + MCP） |

### `Awesome Hook/`

空目录，预留 Hook 样例。Cursor/Claude hook 的现货在 `Trellis/kit/` 与 `trellis_origin` 平台模板里。

---

## 10. 其它顶层

| 路径 | 作用 |
|------|------|
| `computer/` | Cloudflare `@cloudflare/computer`：Durable Object 上 SQLite 虚拟文件系统（预览，非生产）。看 `packages/computer/` · `docs/` · `examples/` |
| `本地环境问题.md` | **本机** Windows：`python3` Store 桩、GBK、Git Bash vs cmd。跑 `trellis_origin` 测试失败先读 |
| `_find-paperclip-locks.ps1` | 查找 Paperclip 锁文件的辅助脚本 |
| `.claude/` | 本仓级 Claude 配置（若有） |

---

## 11. 容易搞混的对照

| A | B | 别混 |
|---|---|------|
| `Trellis/` | `trellis_origin/` | 安装包 vs 上游源码 |
| `codegraph` | `code-graph-rag` | 轻量本地 MCP vs Memgraph 重栈 |
| `chrome-devtools-mcp` | `agent-browser` | CDP/DevTools MCP vs Rust 浏览器 CLI |
| `pi` | `pi-gui` | Agent harness vs 桌面壳 |
| `herdr` | `loopx` | Agent 终端 multiplexer（托管 Claude/Codex 等 pane）vs 长跑 Agent 控制面 |
| `ralph` | `loopx` | bash 循环反复 spawn Claude/Amp 清上下文跑 PRD story vs 通用长跑控制面 |
| `ralph` | `Trellis/` ClosedLoop | 单仓 PRD 自动迭代脚本 vs Trellis 多 lane / 证据门禁体系 |
| `herdr` | `pi` / `pi-gui` | 不替换现有 agent，只拥有它们的终端 vs 自己就是 harness / 桌面壳 |
| `deepseek-harness` | `pi` | DeepSeek 插件化 `dsh`（Cordis，Web UI）vs Pi coding-agent harness |
| `CLI-Anything` | `OpenCLI` | 给已有桌面/专业软件包一层 Agent CLI（Hub+harness）vs 把网站/登录 Chrome 变成 CLI + Browser Use |
| `llmfit` | `Switchyard` | 估本机「哪个模型跑得动」vs LLM 流量代理/协议翻译 |
| `superpowers` | `ECC` | obra 方法论 skill 包 vs 多平台 harness OS（skills+hooks+memory+security） |
| `ECC` | `Trellis/` | 通用 harness 增强 vs 项目 Task/RDV/archive 交付链 |
| `Awesome Design/ui-ux-pro-max` | skill example README 里的同名条目 | 实体只在 Design 目录 |
| `Agent Test/` | `requirement-driven-verification` | 协议文档 vs 可执行 skill |
| `architecture-explainer` | `Tech-Doc-Style-Chinese` | 把架构讲懂（教学+术语） vs 中文技术文案克制改写 |
| `architecture-explainer` | `brainstorming` | 解释已有方案、禁止改设计 vs 创意前先设计、禁止先写代码 |
| `caveman` | `ECC` | 省 token 的 wrap/skill vs 整包 harness OS（hooks+skills+memory） |
| `caveman` | Trellis 轻量主线 | 可选 token 压缩 overlay vs Task/RDV/archive 交付链（勿盲目叠装） |
| `strix` | `Agent Test/` / RDV | 外部应用安全 pentest vs 本仓需求是否交付 |
| `dbx` | `corsair` | 数据库客户端 + DB MCP vs SaaS 集成层（Gmail/Slack…） |
| `docling` | `markitdown` | 重型文档布局/结构解析 vs 轻量多格式转 Markdown |
| `Anthropic-Cybersecurity-Skills` | `strix` | 817 域安全 skill 知识库 vs 可执行 pentest runtime |
| `plan-review-mcp` | `trellis-preflight` | 审 Plan/PRD 文本 vs 审本仓库依赖是否就绪 |

---

维护：新增克隆项目时，在对应分类 README 索引加一行，并在本稿加一行「作用 + 先打开哪个文件」。
