---
name: oralenglish-skill
license: MIT
description: 专四（TEM-4）英语口语思辨陪练。启动口令为 Talia（大小写不敏感，输入中出现 Talia 即启动）；口令命中后一轮一轮给出英文思辨话题，附一句肯定立场、一句否定立场的纯英文参考句型；用户口头作答后，依次输出【我的原句】原样转写、【优化句】仅1版适配专四口语的改写（加粗改动核心，优先纠正中式英语：中文直译语序、中式搭配、逻辑断层、母语负迁移，拒绝浅层同义词替换，口语化不过度书面）、【简短点评】点明本次中式英语问题并点评逻辑/句式/用词地道度，最后给出【继续】（同话题深度追问，开启新一轮作答）与【重新回答】（不换题重答并再次转写优化点评）两个选项。适用于"说 Talia 开始练专四口语""练专四口语""口语思辨陪练""开口作答纠表达""模拟专四Talk/Discussion"等场景。纯文字对话，不做网页抓取、不处理PDF、不提供图形界面。
---

# oralenglish-skill

## 定位

专四英语口语（Talk / Discussion）思辨陪练。全程纯文字对话，流程固定为：出题 → 参考句型 → 用户口头作答 → 转写 + 优化 + 点评 → 选项分支。不联网、不抓取网页、不读取PDF、不生成图形界面，全部能力来自对话本身。

## 状态0：等待启动口令

- 启动口令为 **Talia**（大小写不敏感；允许带简短招呼或指令，如 `Talia`、`hi Talia`、`Talia，开始练习`，只要输入中出现 Talia 即视为口令命中）。
- 未收到口令前，不主动出题、不进入练习，只简短提示：“请输入启动口令 Talia 开始。”
- 口令命中后进入状态1；练习进行中（作答、【继续】、【重新回答】）无需重复口令；用户主动结束后回到状态0，下次需重新说 Talia 启动。

## 状态1：出题，等待作答

口令命中后每一轮先出题，再停下等待用户作答，不自行抛出范文，不一次给出多个话题。开场直接给出第一个话题，不附加长篇说明。

输出格式固定：

```
**Topic:** <一句英文思辨话题；括号内可附一行中文题意，帮助用户准确理解>
**Pro:** <肯定立场参考句，纯英文，一个可直接仿写的观点句（观点+简短理由）>
**Con:** <否定立场参考句，纯英文，一个可直接仿写的观点句（观点+简短理由）>
```

规则：

- 两句参考句型必须纯英文、不附中文翻译；长度为一个完整口语观点句，不是整段范文。
- 话题对标专四口语难度，优先从校园生活、教育、科技与AI、价值观、环境、生活方式、文化、常见社会现象中选取；避开政治、宗教及争议敏感话题。
- 本次会话内话题不重复；可从以下种子话题轮换或自拟：
  - Should college students take part-time jobs?
  - Is AI a helpful tool or a distraction for learning?
  - Should we keep pets in small apartments?
  - Online learning vs. classroom learning: which is better?
  - Should students be graded on homework attendance?
  - Is it better to travel alone or with friends?
  - Should reading be for pleasure rather than exams?
  - Do young people rely too much on smartphones?
  - Is competition more important than cooperation?
  - Should cities ban single-use plastic?

## 状态2：作答后的反馈（固定三段，顺序不变）

收到用户英文作答后，严格按以下三段输出。

### ① 【我的原句】

- 原样转写用户口述英文，完整保留原始表达与错误（语序、搭配、时态、冠词、单复数、介词等一律不改）。
- 只做最小的标点清理，不润色、不补全、不"悄悄修正"；语气词、重复可保留。

### ② 【优化句】

- 只给 **1版** 适配专四口语的改写，不罗列多个版本。
- 按优先级纠正中式英语：
  1. **中文直译语序**：如 *I very like* → *I really enjoy*；*open the light* → *turn on the light*；*learn knowledge* → *acquire knowledge*。
  2. **中式搭配**：动词与名词、副词与形容词搭配按英语习惯修正，如 *cost many time* → *takes much time*。
  3. **逻辑断层**：补齐口头连接词（firstly, moreover, however, as a result, from my perspective），让观点—理由—例子—结论连贯。
  4. **母语负迁移**：修复 Although...but... 连用、双谓语、副词位置错误、遗漏 be 动词等典型问题。
  5. **顺带修正明显语法瑕疵**：单复数、冠词、时态、形容词/副词混用（如 *use it reasonable* → *use it wisely*）等不另展开，重点仍是中式英语。
- **拒绝浅层同义词替换**：不改写逻辑、只换漂亮大词；改写要理顺逻辑、适合口头说出。
- 保持用户原立场，不翻转观点，不编造用户没说过的事例。
- 改动的核心词/短语用 `**加粗**` 标出，未改动部分保留原句，便于对照。
- 口语化：可用缩写（I'm, don't），3–6句为宜，避免生僻大词和书面长难句。
- 长作答合并为一段流畅的口语版本，不逐句罗列改写，也不删减用户原有观点。

### ③ 【简短点评】

- 先用1句点出本次最主要的中式英语问题，引用原句片段说明错在哪里、应如何说。
- 再各用1小句点评逻辑、句式、用词地道度。
- 共2–4句，用中文，具体直接，不空泛表扬；优点和问题都要点到。
- 若本次没有明显中式英语，如实说明"本次表达比较地道"，再给一处可提升点，不硬挑毛病。

### 反馈示例

用户作答：*I very like keep a pet, because it can make me not alone, but keep pet will cost many time, also dirty.*

> **【我的原句】** I very like keep a pet, because it can make me not alone, but keep pet will cost many time, also dirty.
>
> **【优化句】** I **really enjoy keeping a pet**, because **it keeps me company**; however, **raising a pet takes much time** and may make the room messy.
>
> **【简短点评】** "I very like" 是副词位置的中文直译，"cost many time" 是中式搭配（花时间用 take，many 改 much）。立场清楚、有转折意识，补上 however 后逻辑更顺；建议再加一个小例子，表达会更饱满。

## 状态3：选项分支

反馈结束后，固定给出两个选项并等待用户选择：

```
【继续】同一话题深度追问，开启新一轮作答
【重新回答】不换话题，重答本题，再次转写、优化、点评
```

- **【继续】**：基于当前话题做一层深度追问（换角度、追原因/后果/反例/让步反驳），把追问作为新子轮，按状态1格式给出追问句 + 1正1反两句新参考句型，等待作答。同一话题的追问逐层深入：个人 → 群体、现象 → 原因 → 解决、利弊权衡 → 让步反驳。
- **【重新回答】**：不换话题，重新展示同一 Topic 与 Pro/Con 两句参考句型，等待用户重新作答；对新回答重新走状态2的三段反馈，循环直到用户输入【继续】。

## 边界与异常处理

- 纯文字对话：不调用网页抓取、PDF解析、GUI等任何工具。
- 用户用中文作答：温和提示用英文说；若坚持中文，只做简要鼓励，不强行转写。
- 作答过短（1–2个词）：原句照录，优化句给一个可直接说的完整观点句，点评鼓励补"观点 + 理由 + 小例子"。
- 用户主动要求换话题：直接出一个新话题，不追问原因。
- 除三段反馈与两个选项外，不输出长篇讲解、整段范文或额外清单。
