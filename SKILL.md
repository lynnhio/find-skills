---
name: find-skills
description: 查找、比较和按用户授权安装 Agent Skills。适用于“找一个能做某任务的 Skill”“有没有相关技能”“搜索 OpenClaw/ClawHub 技能”等请求；覆盖 skills.sh、ClawHub、SkillHub、OpenClaw Directory、LobeHub、GitHub 和公开社区来源。
metadata:
  upstreams: "https://github.com/vercel-labs/skills/tree/main/skills/find-skills ; https://clawhub.ai/fangkelvin/skills/find-skills-skill"
  repository: "https://github.com/lynnhio/find-skills"
  maintenance: "Merged custom skill; preserve all discovery sources when updating."
---

# Find Skills

按用户的任务、运行平台和依赖要求发现 Skill，核对真实源文件后推荐。合并 Vercel Skills 生态与 fangkelvin 的 OpenClaw 多来源发现指南，保留双方的全部检索来源。

## 来源

| 来源 | 地址与用途 | 检索方式 |
| --- | --- | --- |
| skills.sh | https://skills.sh/ — 榜单、安装量、Skills CLI 生态 | 先看相关榜单；用 `skills find` 搜索，可按 GitHub owner 限定 |
| ClawHub | https://clawhub.ai/ 、https://clawhub.com/ — OpenClaw Skill 注册表 | `clawhub search` 搜关键词，`explore` 浏览，`inspect` 读取文件和版本 |
| SkillHub | https://www.skillhub.cn/ — 中文社区与上游镜像 | 搜中文和英文关键词；核对 namespace、作者、版本及上游链接 |
| OpenClaw Directory | https://www.openclawdirectory.dev/skills — OpenClaw 分类目录 | 按类别、功能或名称寻找，再返回原作者源文件核验 |
| LobeHub Skills Marketplace | https://lobehub.com/skills — 社区技能市场 | 站内搜索或公开页面检索，核对作者与上游 |
| GitHub | https://github.com/search — 原作者仓库和 `SKILL.md` | 搜 `openclaw skill`、`agent-skill`、任务关键词或 `path:SKILL.md` |
| SitePoint Community | https://www.sitepoint.com/community/ — 社区线索 | 搜公开讨论中的技能名称与仓库链接，返回源仓库核验 |
| Clawd Discord | https://discord.com/invite/clawd — 社区线索 | 使用有权读取的消息或公开索引；需登录且无法读取时报告未检查 |

GitHub 的原有候选入口一并保留：[vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)、[anthropics/skills](https://github.com/anthropics/skills)、[microsoft](https://github.com/microsoft)、[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)。它们是检索入口，具体 Skill 仍需逐项核验。

SkillHub 与 ClawHub 可能指向同一上游；保留两个发现来源，按原作者、仓库路径或注册表标识归并同一候选，避免把镜像计为两个独立 Skill。上游内容冲突时报告版本和差异，不静默混用。

## 检索与核验

1. 从已有上下文确定任务、目标平台和约束。关键词尽量具体，例如 `react testing`、`document`、`web search`、`tavily`、`github`、`calendar`；无结果时尝试同义词及中英文名称。
2. 未指定来源时先看 skills.sh 的相关榜单并搜索 Skills CLI；OpenClaw 请求优先查询 ClawHub。按覆盖不足扩展到表中其他来源。用户点名某来源时先查该来源；要求全面检索时逐一记录全部来源的结果、失败或未访问原因。保留所有入口不代表每次请求都必须访问所有网站。
3. 读取候选的真实 `SKILL.md`、支持文件及安装说明，确认适用平台、依赖、凭据需求和是否会产生写入。目录摘要、搜索命中或热度不能替代源文件核验。
4. 核对安装量、作者身份、仓库 stars、维护情况和来源一致性。延续原版的筛选参考：优先查看安装量达到 1,000 的候选；低于 100 次安装或仓库少于 100 stars 时增加核验。热度只是辅助信号，不能证明安全或适用，也不能单凭低热度否决明确匹配的候选。数值须注明来源与查询时间，不沿用旧示例中的统计。
5. 推荐时列出名称、用途、平台、原作者、发现来源、核验过的源链接、版本、依赖、热度数据及匹配理由。给出针对该 Skill 的安装方式；只读发现请求到此结束。已有安装授权则继续完成授权范围，不重复确认。

遇到限流、网络或登录限制时，说明失败来源，并用表中其他公开来源补充。没有结果与没有访问成功分别报告。仍无匹配时说明查过的来源，可直接帮助完成用户任务；只有用户希望创建 Skill 时才进入创建流程。

## CLI 用法

优先使用已安装且已核对版本的 CLI。需要临时调用时固定包版本，先检查对应 `--help`；以下版本在 2026-10-13 合并时核对，后续升级重新核验参数。

```bash
# Skills CLI：按任务或作者检索
npx --yes skills@1.7.2 find "react testing"
npx --yes skills@1.7.2 find "react" --owner vercel

# ClawHub：按功能或服务商检索
npx --yes clawhub@0.23.3 search "web search" --limit 5
npx --yes clawhub@0.23.3 search "tavily" --limit 5

# 按热度浏览与读取源文件，均不安装 Skill
npx --yes clawhub@0.23.3 explore --sort downloads --limit 5
npx --yes clawhub@0.23.3 inspect @fangkelvin/find-skills-skill --files
```

按 stars 或安装量比较时读取候选元数据或网页统计，注明各来源的统计口径。上游原文中的 `clawhub browse`、`search --sort installs` 和 `search --sort stars` 不作为已核验命令使用；用当前 `explore --help` 和元数据选择支持的方式。

搜索方向保留两版的范围：Web 开发、测试、DevOps、文档、代码质量、设计、效率、天气、系统维护、服务集成、搜索和 Agent 自动化。例词包括 `react`、`playwright`、`docker`、`changelog`、`accessibility`、`weather`、`healthcheck`、`feishu`、`notion`、`proactive-agent`；例词不是已安装或推荐结论。

## 安装与维护

安装需要用户授权。读取当前安装、目标目录和同名条目后，安装指定候选；安装一个 Skill 不授权安装其他候选、升级全部 Skill 或修改其他平台。

安装前识别目标客户端的 Skill 目录，以及用户已有的主源和运行入口约定。存在统一主源时，将下载 Skill 与自建或合并 Skill 分开管理，运行入口按客户端支持的方式指向主源；没有统一主源时使用目标客户端的标准安装目录。项目安装和其他平台按用户指定范围处理。

常用安装方式保留 Skills CLI 的 `skills add <owner/repo@skill>` 和 ClawHub 的 `clawhub install @owner/slug --version <version>`。执行前检查命令的目标路径和作用范围，避免其默认目录与正式主源冲突；`-g -y` 仅在用户已授权全局安装且目标布局正确时使用。不使用会覆盖本机既有布局的无差别安装。

同名安装先比较来源和内容。更新只针对已授权的 Skill；`skills check` 可检查受其管理的上游版本，`skills update` 或 `clawhub update` 会写入，不能当成只读检查。此合并版由自定义主源维护，不使用任一上游的自动更新直接覆盖。

安装后运行适用的 Skill validator，逐文件回读主源，核对运行入口的真实路径。文档校验、源哈希一致、CLI 检索成功和运行时加载是不同证据，按实际完成范围报告。Codex 在下一轮重新读取 Skill；未单独同步的平台不得称为已同步。

本 Skill 负责发现与获授权的安装。创建新 Skill 使用 `skill-creator`；查看既有 OpenClaw 安装可使用 `openclaw skills list`，须先确认本机命令可用。
