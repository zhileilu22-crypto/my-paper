# 技能与依赖审计

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

