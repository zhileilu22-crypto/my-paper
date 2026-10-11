# 技能与依赖审计

## 当前云环境安装记录（2026-10-11）

### GPT-6 Solar 项目适配（2026-10-11）

- 保留 177 个 Scientific Agent Skills 入口及全部配套文件；ARS 保留根技能、六个工作流及核心脚本。项目新会话建议 `gpt-6-sol` / `high`，但当前会话的实际模型取决于运行环境和用户选择。
- ARS 模型路由、运行策略、团队说明和可选规划器清单已同步改用 Solar。`ars-lit-review`、`ars-citation-check`、`ars-reviewer` 和 `ars-plan` 的规划测试均找到全部必读文件，规划模型为 `gpt-6-sol`；复杂任务默认 `high`，常规规划为 `medium`。
- ARS 路由、单根技能和 hook 安全三项静态检查通过；178 个技能入口的 YAML 元数据可解析且名称与目录匹配。未运行实际 Solar 模型质量基准，未验证此会话的实际模型。
- 仅裁剪 ARS 上游历史评测的 `runs/raw/`（390 个文件）和 `runs/superseded/`（13 个文件），约 12.6 MB。论文和文献工作流不使用这些历史评测输出；以后运行上游完整评测需从固定提交恢复。
- 上游 `all` 质量检查需完整插件仓库的 `.codex-plugin/plugin.json`，直接技能安装不含该文件；因此本次改用适合直接安装的专项检查，不将 `all` 检查记为通过。

- 在 `.agents/skills/` 安装 Scientific Agent Skills 的 177 个技能，以及 ARS-Codex 的 `academic-research-suite` 根技能与完整资源，共 178 个入口。
- 上游来源、精确提交和许可证见 `docs/skill-sources/installed.json`；使用方式见 `docs/SKILLS_USAGE.md`。
- 178 个入口 YAML 解析、名称唯一性、目录名匹配、完整文件复制校验通过；ARS 六个工作流入口存在。
- ARS 官方 `root-router` 和 `single-root-skill` 检查通过。
- PDF 核心预检、sidecar 与 CLI 的 52 项测试全部通过；完整 PDF 测试共 80 项，78 项通过、2 项失败。失败涉及可选内容分类沙箱的进程回收：失败后检查发现两个子进程均为父进程 PID 1 下的僵尸进程，测试使用 `os.kill(pid, 0)` 将其判为仍存在。当前容器的回收行为与上游测试预期不符；未修改上游测试或源码，默认未启用内容分类功能。
- Scientific Writing 的本地脚手架 CLI 可启动并显示参数；未生成论文正文，未执行所有科学工具的端到端验证。
- 当前环境可导入 PyYAML 和 pypdf；其他科学软件、外部 API、Nature skills 未在本次安装中验证或安装。
- 新会话中的技能注册状态仍需由实际技能清单确认，不将文件存在等同于注册成功。

## 历史环境审计（以下不代表当前云环境）

审计时间：2026-09-05（Asia/Shanghai）

判定原则：只有出现在当前会话“Available skills”清单中的技能才记为“已识别、可调用”；仅凭目录或 `SKILL.md` 存在不判定为安装成功。

## 当前会话已识别

### ARS-Codex

- `academic-research-suite`：已识别、可调用。
- 文件位置：`.agents/skills/academic-research-suite/SKILL.md`。
- 说明：用户所称 `academic-research-skills-codex` 在当前项目中以 `academic-research-suite` 这一根路由技能注册，元数据标明 `upstream_suite: academic-research-skills`、`codex_adapter: true`。
- ARS 内部 `deep-research`、`academic-paper`、`academic-paper-reviewer`、`academic-pipeline`、`experiment-agent`：只是由根技能按需读取的 `WORKFLOW.md`，未作为当前会话中的独立技能注册；但可通过 `academic-research-suite` 路由执行。

### Nature skills

以下 9 个均已出现在当前会话技能清单中，因此已识别、可调用：

- `nature-academic-search`
- `nature-citation`
- `nature-data`
- `nature-figure`
- `nature-paper2ppt`
- `nature-polishing`
- `nature-reader`
- `nature-response`
- `nature-writing`

个人安装位置为 `/Users/leillll/.codex/skills/nature-*`。项目内 `nature_skills/skills/nature-*` 是源副本；它们的存在本身不作为本次“已识别”结论的依据。

## 当前任务所需依赖

- Poppler：`pdfinfo`、`pdftotext`、`pdftoppm` 均可用。
- Tesseract OCR：可用，已安装 `chi_sim` 和 `eng` 语言数据。
- Codex bundled Python：`pypdf`、`pdfplumber`、`python-pptx`、`Pillow` 可用。
- 系统 Python：`PyMuPDF/fitz`、`matplotlib`、`python-pptx`、`Pillow` 可用。
- PDF 结构预检：使用 bundled Python 后运行成功，两份标准均为 PASS。

## 缺失或受限依赖

- `Rscript`：缺失。若以后选择 R 作为 `nature-figure` 后端，将无法渲染，需先安装 R；该技能禁止自动改用 Python 替代。
- 系统 Python 中 `pypdf`、`pdfplumber`、`PyYAML`、`seaborn`：缺失。
- Codex bundled Python 中 `PyYAML`、`PyMuPDF/fitz`、`matplotlib`、`seaborn`：缺失。当前 PDF 工作通过系统 Poppler、Tesseract和 bundled `pypdf/pdfplumber` 已完成，不受影响。
- `skill-creator` 的 `quick_validate.py` 因两个 Python 环境均缺少 `PyYAML` 而不能直接运行；Nature 技能 YAML frontmatter 已用系统 Ruby YAML 解析器验证。
- `nature-academic-search` 所列专用 PubMed、CrossRef、arXiv、Semantic Scholar 等 MCP 工具未暴露在当前工具清单中，因此不能按其专用 MCP 路径调用。当前会话有网页检索能力，可在具体文献任务中按权威来源降级执行，但这不等同于专用 MCP 已安装。
- Semantic Scholar、NCBI 等可选 API key：未检查，也不是本次项目初始化的必需依赖。

## 尚未做运行级验证

- 本次只实际验证了 ARS PDF 预检与 PDF/OCR 工具链。
- Nature 的写作、润色、引用、数据声明、绘图、PPT、论文阅读和审稿回复尚未逐项执行端到端样例。
- `nature-citation` 和 `nature-academic-search` 的联网脚本/API 限流、密钥与返回质量尚未验证。

