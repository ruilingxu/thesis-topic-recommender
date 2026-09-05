# 毕业论文选题推荐助手（Thesis Topic Recommender）

从官方毕业论文选题里，按你的研究方向、简历关键词、偏好导师做加权打分，推荐 Top 5 选题并生成可直接使用的邮件模版。

## 它做什么

- 读取 ESCP Berlin 硕士项目的官方选题 Excel（结构：导师 / 邮箱 / 院系 / 校区 / 研究领域 / 研究方法 / 选题标题 / 简述 / 参考文献 / 先决条件 / 可选状态等）
- 4 阶段流程：信息收集（可选）→ 数据读取与加权打分 → Top 5 结构化推荐（含匹配理由）→ 生成带导师邮件模板的 Shortlist Excel
- 打分维度：研究方向匹配、简历关键词匹配、偏好导师、项目/校区等，均为加权计分
- 全部输出中文、结构化分点；只推荐 Excel 中真实存在的选题，不编造

## 安装与体验（需要 Claude Code）

```bash
mkdir -p ~/.claude/skills
cp SKILL.md ~/.claude/skills/thesis-topic-recommender/
```

在 Claude Code 里说类似：
> 用 thesis-topic-recommender 帮我从毕业论文选题里推荐 5 个，我研究方向是 AI + 可持续发展，这是简历 [PDF]

## 关于数据文件（重要）

Skill 依赖官方选题库，**不在本仓库分发**。请：

1. 打开 `SKILL.md`，把 `{EXCEL_PATH}` 换成你本机选题 Excel 的路径
2. 运行时把 Excel 放在该路径即可（Skill 每次实时读取，不缓存）

## 免责声明

选题可用性请以导师确认为准；邮件模板需你本人核对后再发送。
