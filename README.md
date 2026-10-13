# find-skills

用于查找、比较和按用户授权安装 Agent Skills 的中文 Skill。融合 Vercel 的 skills.sh / Skills CLI 工作流与 fangkelvin 的 OpenClaw 多来源发现指南。

## 保留的来源

skills.sh、ClawHub、SkillHub、OpenClaw Directory、LobeHub Skills Marketplace、GitHub、SitePoint Community、Clawd Discord。

保留榜单、安装量、作者和仓库质量核验；同一 Skill 在不同目录或镜像出现时归并候选，同时保留发现来源。用户要求全面检索时逐一报告各来源结果和访问限制。

## 安装

通过 Skills CLI 安装，按提示选择客户端与安装范围：

```bash
npx --yes skills@1.7.2 add lynnhio/find-skills --skill find-skills
```

也可以将本仓库文件放入目标客户端支持的 Skill 目录。已有统一主源时遵循自己的主源与运行入口约定。

## 使用

在支持 Agent Skills 的客户端中提出请求，例如：

- “帮我找一个生成发票的 Skill。”
- “搜索适合文档处理的 OpenClaw 技能。”
- “从全部来源找 React 测试 Skill，并比较作者、依赖和维护情况。”

完整工作流见 [SKILL.md](SKILL.md)。本仓库是供 Agent 读取的指令文档，CLI 检索可使用文档列出的固定版本；部分来源也支持公开网页检索。

## 来源与维护

- [Vercel find-skills](https://github.com/vercel-labs/skills/tree/main/skills/find-skills)
- [fangkelvin find-skills-skill v1.0.0](https://clawhub.ai/fangkelvin/skills/find-skills-skill)
- [SkillHub 原始发现入口](https://www.skillhub.cn/skills/clawhub_fangkelvin/find-skills-skill)

由 [lynnhio](https://github.com/lynnhio) 合并维护。更新时保留全部来源；不要用任一原版的自动更新直接覆盖合并内容。

上游署名及许可说明见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
