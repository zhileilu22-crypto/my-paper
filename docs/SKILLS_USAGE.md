# 论文研究技能使用说明

安装日期：2026-10-11。安装范围为当前仓库，位置为 `.agents/skills/`。

## 已安装套件

- Scientific Agent Skills：来自 https://github.com/K-Dense-AI/scientific-agent-skills ，完整安装 177 个技能及配套文件。MIT 许可证。
- Academic Research Skills：使用官方 Codex 适配版 https://github.com/Imbad0202/academic-research-skills-codex ，安装 `academic-research-suite` 根技能及完整 ARS 工作流。CC BY-NC 4.0 许可证，使用时须遵守署名及非商业用途条件。

精确提交、来源及技能列表见 `skill-sources/installed.json`，两套许可证和上游说明保存在 `skill-sources/`。安装未启用外部模型、自动网络调用、Claude hooks 或上游的模型配置。

## 如何使用

在此仓库中开启新的 Codex 会话，让客户端重新扫描技能；检查技能清单是否出现 `academic-research-suite`、`scientific-writing` 等名称。文件安装和静态验证已完成，但本次会话没有重新注册的证据；不能把文件存在说成已注册。

可用请求示例：

- “使用 $academic-research-suite，整理考古纹样修复的文献研究方案，暂不写正文。”
- “使用 $literature-review，核对这些文献的证据、差异和研究空白。”
- “使用 $scientific-critical-thinking，检查我的研究方法和评价指标。”
- “使用 $scientific-visualization，根据我提供的数据制作论文图表。”
- 明确解除项目正文限制后，才使用 `$scientific-writing` 或 ARS 写作流程生成正文。

按任务读取一个技能及其必要资源，不一次加载全部套件。ARS 内部工作流通过根技能路由，不作为独立 Skill 注册。当前课题和授权边界以仓库 `AGENTS.md` 为准。

技能文件安装不等于所有科学软件和数据库均可运行。具体分析、绘图或检索任务开始时再检查对应依赖、网络权限与 API 配置；不要在聊天中提供密钥。当前安装没有要求 API 密钥。

## 验证与更新

本次检查：178 个技能入口的 YAML 元数据、名称唯一性、目录名匹配、复制文件与固定上游提交逐字节一致，以及 ARS 六个工作流入口完整性。ARS 官方 `root-router` 和 `single-root-skill` 检查通过。运行级结果见根目录 `SKILL_AUDIT.md`。

更新时保留当前项目修改，先获取新版本到仓库之外的临时目录、比较变更，再更新技能和来源记录；不要直接覆盖已有修改。云任务已有隔离环境，使用现有 checkout，不创建 Git worktree。
