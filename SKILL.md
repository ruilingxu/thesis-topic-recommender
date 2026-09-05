---
name: "thesis-topic-recommender"
description: "Recommends thesis topics from ESCP MSc programmes thesis topics Excel file based on user's research interests, CV, preferred supervisors, and research methods. Invoke when user wants thesis topic recommendations or help choosing a thesis topic."
---

# Thesis Topic Recommender (毕业论文选题推荐)

This skill helps students find the best thesis topics from the ESCP MSc programmes thesis topics Excel file, based on their personal preferences and background. It also supports generating a structured Shortlist Excel output for final selection.

## ⚙️ 配置区 (Configuration)

**⚠️ 首次使用前请修改以下路径：**

| 配置项 | 变量名 | 当前值 |
|--------|--------|--------|
| **选题数据源路径** | `{EXCEL_PATH}` | `/Users/a1013/Documents/trae_projects/毕业论文/2026_2027_Thesis topics  Msc programmes.xlsx` |

修改后，本文件中所有引用 `{EXCEL_PATH}` 的位置将自动使用新值。

## 👋 使用指南 (Getting Started)

**当用户第一次调用此 skill 时，必须先输出以下引导说明，再进入正式流程。**

---

欢迎使用毕业论文选题推荐工具！本工具将帮助您从 ESCP 校区的 1251 个毕业论文选题中，智能筛选出最适合您的 5 个选题，并为每个选题生成发给导师的邮件模板。

### 🔄 流程概览（共 4 个阶段）

| 阶段 | 内容 | 您需要做什么 |
|------|------|-------------|
| **Phase 1** | 信息收集 | 回答 4 个可选问题（研究方向、简历/背景、偏好导师/校区、研究方法/项目） |
| **Phase 2** | 数据分析 | 自动读取 Excel，按您的偏好筛选评分 |
| **Phase 3** | 推荐输出 | 查看 5 个推荐选题的详细分析（推荐原因、对您的好处、职业发展帮助） |
| **Phase 4** | Shortlist 生成 | 选定心仪选题后，生成结构化的 Excel Shortlist 文件 |

### 💡 您需要怎么配合

**Phase 1 — 信息收集阶段：**
- ✅ **回答问题即可**：每题均可多选，也可随时说"跳过"
- ✅ **提供简历更佳**：上传 PDF/Word/文本简历，我会从中提取关键词进行匹配
- ✅ **已提供的信息无需重复**：如果您在初始消息中已说明部分信息，我会直接使用

**Phase 2-3 — 分析与推荐阶段：**
- 📖 仔细阅读每个推荐选题的分析
- 🤔 如有疑问，随时提问（如"这个选题的导师还有其他类似话题吗？"）
- 🔁 可以反复调整偏好重新筛选

**Phase 4 — Shortlist 生成阶段：**
- 📋 告诉我您想纳入 Shortlist 的选题（可指定编号、标题，或让我从对话历史中自动提取）
- 🏷️ 提供一个命名标识（如您的姓名），用于文件命名

### ⚡ 快速开始

如果您想跳过信息收集直接浏览选题，只需告诉我您的**项目**和**研究方向**，我会基于最少必要信息为您推荐。

---

**现在，让我们开始吧！** 首先，请告诉我您感兴趣的研究方向有哪些？（可多选，也可跳过）

---

（输出完以上引导说明后，自动进入 Phase 1 信息收集流程）

## Data Source

The thesis topics Excel file is located at:
``

### Excel Structure (columns in order):
| Index | Column | Description |
|-------|--------|-------------|
| 0 | Supervisor | 导师姓名 |
| 1 | Email address of supervisor | 导师邮箱 |
| 2 | Academic Department | 学术院系 |
| 3 | Campus of Professor | 导师所在校区 |
| 4 | Topic area | 研究领域 (e.g. Sustainability, AI, Diversity, Leadership, Finance, Marketing, Supply Chain, etc.) |
| 5 | Qualitative/Quantitative research methods | 研究方法 (Qualitative/Quantitative/Mixed/Both/Case Study etc.) |
| 6 | Title or topic | 选题标题 |
| 7 | Short Description of topic | 选题简述 |
| 8 | Literature | 参考文献建议 |
| 9 | Prerequisites | 先决条件 |
| 10 | Comment | 备注 |
| 11 | Availability | 可选状态 (green=available, red=unavailable) |
| 12 | MISM | 适用于 MISM 项目 (x=是) |
| 13 | SUSTM | 适用于 SUSTM 项目 (x=是) |
| 14 | MSEI | 适用于 MSEI 项目 (x=是) |
| 15 | MSDB | 适用于 MSDB 项目 (x=是) |

### Data Summary:
- Total topics: ~1251
- Unique supervisors: ~47
- Campuses: , Madrid, Paris
- Programs: MISM, SUSTM, MSEI, MSDB
- Research methods: Qualitative, Quantitative, Mixed, Case Study, Literature Review, etc.

## Workflow

### Phase 1: Information Gathering (信息收集) — OPTIONAL FIELDS

Collect user preferences to enable personalized recommendations. **ALL questions are optional** — users may skip any question by saying "跳过" or simply not providing an answer. If a user has already provided some information in their initial message, skip the corresponding question.

**Question 1 — 研究方向 (Research Direction):**
Ask the user about their research interests/direction. Provide common options based on the data:
- Sustainability / 可持续发展
- Artificial Intelligence / 人工智能
- Diversity & Inclusion / 多元化与包容
- Leadership / 领导力
- Finance / 金融
- Marketing / 市场营销
- Supply Chain Management / 供应链管理
- Entrepreneurship / 创业
- Strategy / 战略管理
- Human Resource Management / 人力资源管理
- Tourism / 旅游
- Other (user specifies)

Users can select multiple options. If they skip, note "无偏好" and proceed.

**Question 2 — 简历匹配 (CV Matching):**
Ask the user to share their CV/resume or briefly describe their academic background, work experience, and key skills. Tell them: "您可以上传简历（PDF/Word/文本），或直接描述您的学术背景、工作经历和核心技能。如果跳过此问题，将仅基于选题本身进行推荐。" If they skip, proceed without CV matching.

**Question 3 — 偏好导师与校区 (Preferred Supervisor & Campus):**
Ask the user if they have any preferred supervisors or supervisors they want to avoid. Also ask which campus they prefer (/Madrid/Paris). If they skip, note "无偏好" and proceed.

**Question 4 — 研究方法与项目 (Research Method & Programme):**
Ask:
1. Preferred research methods: Qualitative / Quantitative / Mixed Methods / No preference
2. Which MSc programme they are enrolled in (MISM/SUSTM/MSEI/MSDB)

If they skip, note "无偏好" for both and proceed.

### Phase 2: Data Loading & Analysis (数据加载与分析)

After collecting user preferences (even partially), load and analyze the Excel data using Python. Use your code execution capability to run a Python script that:

1. **Loads the Excel file** from the path above using openpyxl (read_only mode).
2. **Filters topics** based on available user preferences:
   - If programme specified: filter by MISM/SUSTM/MSEI/MSDB column ('x')
   - If campus specified: filter by column 3
   - If research method specified: match against column 5 (normalize to qualitative/quantitative/mixed)
   - If research direction specified: match against column 4 "Topic area" using keyword/substring matching
   - If preferred supervisors specified: prioritize; if avoid list specified: exclude
3. **Scores each topic** based on available user preferences:
   - Research direction match: +3 points (exact), +2 (partial/keyword)
   - Research method match: +2 points
   - Preferred supervisor match: +3 points
   - CV/background alignment: +1 to +3 points (based on keyword matching between CV content and topic description)
   - Programme match: +1 point
   - Campus match: +1 point
   - If NO preferences provided, assign uniform score and proceed to step 4
4. **Ranks topics** by total score and selects the top 5 (or fewer if user requests).
5. **Returns** the full details of the top topics (all columns) as structured output.

**Python script template** (adapt as needed):
```python
import openpyxl
wb = openpyxl.load_workbook('{EXCEL_PATH}', read_only=True)
ws = wb[wb.sheetnames[0]]
rows = list(ws.iter_rows(values_only=True))
# ... filter, score, rank, output top 5
```

**CV handling:** When user provides a CV, read the CV file content using your file reading capability. For PDF files, use Python libraries like pdfplumber or PyPDF2 to extract text. For Word files, use python-docx. For plain text, read directly. Then pass keywords from the CV into the matching script.

### Phase 3: Recommendation Output (推荐输出)

Output the recommended topics. For EACH recommendation, use the following structured format (in Chinese):

---

#### 推荐 N: [选题标题]
**导师:** [Supervisor name] ([Email])
**校区:** [Campus] | **院系:** [Department] | **项目:** [Programme(s)]
**研究领域:** [Topic area]
**研究方法:** [Research method]

**推荐原因:**
- Explain why this topic matches the user's research interests
- Explain how this topic aligns with the user's CV/background (if CV was provided)
- Explain why this supervisor is a good fit (if preferred supervisor was specified)

**对您的好处:**
- What skills/knowledge the user will gain from this thesis
- How it leverages the user's existing strengths
- What unique perspective the user can bring

**对职业发展的帮助:**
- How this thesis topic connects to specific career paths
- Industry relevance and demand for this expertise
- Networking opportunities with the supervisor/industry

**其他重要信息:**
- 先决条件 (Prerequisites): [from column 9, or "无特殊要求"]
- 参考文献 (Literature): [brief summary from column 8, or "请与导师确认"]
- 选题简述 (Description): [summarized from column 7]
- 可用性 (Availability): [from column 11, or "请与导师确认"]

---

After all recommendations, add a **总结与建议 (Summary & Advice)** section that:
1. Summarizes the overall matching strategy
2. Suggests next steps (e.g., contacting supervisors, reading suggested literature, refining research questions)
3. Notes any topics that were close but not selected (honorable mentions)
4. Reminds the user to verify availability with supervisors directly

### Phase 4: Shortlist Generation — Workflow A (自动生成)

This workflow activates when the user says phrases like "生成 shortlist"、"导出 shortlist"、"生成选题清单" or similar requests after receiving recommendations.

**Steps:**
1. Collect the topics the user wants in the Shortlist. This may come from:
   - The user explicitly listing topic numbers/names from previous recommendations
   - Auto-selecting from prior conversation context where the user showed interest
2. For each selected topic, retrieve the full data from the original Excel file (all 16 original columns).
3. Generate a recommendation reason and email template for each topic, based on the user's profile gathered during the conversation.
4. Create an Excel file with the following structure:

**Sheet 1 — 选题推荐** (main sheet, 14 columns):
| Col | Header | Source |
|-----|--------|--------|
| 1 | 序号 | Auto-numbered |
| 2 | 导师 | Original Excel column 0 |
| 3 | 导师邮箱 | Original Excel column 1 |
| 4 | 院系 | Original Excel column 2 |
| 5 | 校区 | Original Excel column 3 |
| 6 | 研究领域 | Original Excel column 4 |
| 7 | 研究方法 | Original Excel column 5 |
| 8 | 选题标题 | Original Excel column 6 |
| 9 | 选题简述 | Original Excel column 7 |
| 10 | 参考文献 | Original Excel column 8 |
| 11 | 先决条件 | Original Excel column 9 |
| 12 | 备注 | Original Excel column 10 |
| 13 | 选择理由 | Generated: why this topic was selected, how it matches user profile |
| 14 | 邮件发送模板 | Generated: personalized email template for contacting the supervisor |

5. Sort topics by supervisor, then by relevance score.
6. Apply professional formatting:
   - Headers: Dark blue background (#2F5496), white bold text
   - Cells: Light borders, top-aligned with text wrapping
   - Column widths: Reasonable widths for each column (reason and email columns wider)
   - Row heights: Auto-sized for content
   - Freeze header row
7. Save the file as: `毕业论文选题推荐Shortlist_{Name}.xlsx` (replace `{Name}` with the user's name or identifier)
8. Inform the user of the file path and provide a summary of the Shortlist.

### Phase 4: Shortlist Generation — Workflow B (手动指定)

This workflow activates when the user directly specifies which topics to include, e.g., "把 X、Y、Z 三个选题做成 shortlist" or "我就选这 5 个：[topic names]".

**Steps:**
1. Parse the user's specified topics. Match them against the original Excel data by title or supervisor name.
2. If a topic cannot be found, inform the user and suggest checking the spelling or providing more details.
3. Once all topics are confirmed, follow the same Excel generation process as Workflow A (steps 2-8 above).
4. The output file follows the same naming convention: `毕业论文选题推荐Shortlist_{Name}.xlsx`.

**Email template generation guidelines:**
- Personalize with the user's actual background (CV highlights, current internship, programme)
- Reference specific aspects of the topic that align with the user's experience
- Include the user's name, programme, and contact email
- Keep the tone professional and concise
- Subject line format: "Thesis Topic Application - [Topic Title]"

**Selection reason generation guidelines:**
- Connect topic to user's research interests (as stated during conversation)
- Connect topic to user's CV/work experience (if CV was provided)
- Highlight unique value the user brings (e.g., industry experience, technical skills, bilingual capability)
- Explain career relevance if discernible from topic

## Important Notes

1. **Language:** All user-facing output MUST be in Chinese (中文).
2. **Output style:** Structured with bullet points and bold subheadings (结构化分点形式，带加粗小标题).
3. **Honesty:** If no topics match the user's preferences well, be honest and explain why. Suggest broadening criteria.
4. **No fabrication:** Only recommend topics that actually exist in the Excel file. Do not invent topics or supervisors.
5. **Data freshness:** Always re-read the Excel file at runtime — do not cache or hardcode topic data.
6. **Single version:** Output only one set of recommendations. Do not provide multiple alternative sets or scenarios.
7. **Mandatory fields in Excel:** The Shortlist Excel MUST include all 19 columns as specified in Phase 4, with proper formatting and the 快速导航 navigation sheet.
8. **File naming:** The Shortlist file MUST be named `毕业论文选题推荐Shortlist_{Name}.xlsx` where `{Name}` is the user's name or an agreed identifier, and saved to the same directory as the Excel data source.
