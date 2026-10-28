# oralenglish-skill

专四（TEM-4）英语口语思辨陪练 Skill：以启动口令 `Talia` 开启，AI 一轮轮给出英文思辨话题和一正一反两句参考句型，用户口头作答后，AI 原样转写、给出 1 版优化句并点评中式英语，支持同题深度追问与原地重答。纯文字对话，零外部依赖。

## 1. 项目解决什么问题

专四口语 Talk / Discussion 需要开口练习，但自习时常见三个缺口：

- **中式英语没人当场纠**：直译语序（I very like）、中式搭配（cost many time）、逻辑断层、母语负迁移等问题，对着范文看不出来。
- **只有通用范文，没有针对本人原句的改写**：不知道自己这句话具体该怎么说、改了哪里。
- **一个话题练完就换，无法往深里想**：缺少同题追问，思辨停在第一层。

本 Skill 在文字聊天里补齐闭环：**出题给支架 → 用户开口 → 原句照录、只优化一版、简短点评 → 【继续】同题深挖或【重新回答】原地重练**。不联网、不读取 PDF、不需要图形界面，文字输入即可完成训练。

## 2. 主要功能

- **口令启动**：以启动口令 `Talia`（大小写不敏感，可带简短招呼，如 `hi Talia`、`Talia，开始`）开启；未说口令时 AI 只提示输入口令，不开始练习；练习过程中无需重复口令，结束后需重新说 Talia 开启下一轮。
- **逐轮出题**：每轮先给出一个英文思辨话题（Topic），紧跟一句肯定立场（Pro）、一句否定立场（Con）的纯英文参考句型，供用户仿写；不一次性抛范文。
- **固定三段反馈**：
  - **【我的原句】**：原样转写用户口述英文，完整保留原始表达与错误，不悄悄修正；
  - **【优化句】**：仅 1 版适配专四口语的改写，按优先级纠正中文直译语序、中式搭配、逻辑断层、母语负迁移，并顺带修正明显语法瑕疵；拒绝浅层同义词替换，改动核心词加粗，保持口语化、不过度书面，不翻转用户立场；
  - **【简短点评】**：2–4 句中文，点明本次主要中式英语问题，再点评逻辑、句式、用词地道度；没有明显错误时如实说明，不硬挑毛病。
- **两个分支**：
  - **【继续】**：基于当前话题做一层深度追问（换角度、追原因/后果/反例/让步），附新的 Pro/Con 句型，开启新一轮作答；
  - **【重新回答】**：不换题，重新展示同一 Topic 与句型，等待重答后再次转写、优化、点评，循环直到【继续】。
- **话题范围**：校园生活、教育、科技与 AI、价值观、环境、生活方式、文化、常见社会现象；避开政治、宗教及争议敏感话题；同一会话内话题不重复。
- **不支持**：网页抓取、PDF 处理、图形界面、语音朗读；全部能力来自对话本身。

## 3. 安装方法

零依赖：不需要安装任何 Python 包，不需要联网，只需复制技能文件夹。

1. 将整个 `oralenglish-skill/` 文件夹复制到客户端的技能目录（Doubao 用户技能目录示例：`.user_skills/`），保持内部结构不变。
2. 刷新或重启客户端，使技能被识别。
3. 触发后即可开始练习，无需额外配置。

目录结构：

```
.
├── README.md
├── LICENSE                       # MIT License
└── oralenglish-skill/
    ├── SKILL.md                  # 技能规则与对话流程（核心）
    └── agents/
        └── openai.yaml           # 技能展示信息：display_name / short_description / default_prompt
```

开发者本地校验（可选）：使用官方 `quick_validate.py` 检查 frontmatter 与命名；Windows 中文控制台需开启 UTF-8 模式：

```powershell
$env:PYTHONUTF8='1'; $env:PYTHONIOENCODING='utf-8'
python quick_validate.py oralenglish-skill
```

## 4. 使用方法

1. **启动**：发送启动口令 `Talia`（大小写不敏感，可带简短招呼，如 `hi Talia`、`Talia，开始练习`）；未说口令时 AI 只提示输入口令，不开始出题。
2. **作答**：口令命中后 AI 给出第一个 Topic 与 Pro/Con 句型，参照句型用英文口头组织回答并输入；回答过短时，AI 会给出可直接说的完整观点句并鼓励补充“观点 + 理由 + 小例子”。
3. **接收反馈**：按【我的原句】→【优化句】→【简短点评】对照学习，重点看加粗的改动处。
4. **选择分支**：
   - 回复 **【继续】**：进入同话题深度追问，答新的子问题；
   - 回复 **【重新回答】**：保留原题重答，AI 对新回答重新转写、优化、点评。
5. 想换话题时直接说明，AI 会出一个新话题；本轮结束后需重新说 `Talia` 开启下一轮。

## 5. 输入输出示例

### 第 1 轮：AI 出题（AI 输出）

> **Topic:** Should we keep pets in small apartments?（小公寓里该不该养宠物？）
> **Pro:** Keeping a pet teaches us responsibility and keeps us company after a long day.
> **Con:** Pets need space and regular care, so small apartments may not suit them well.

### 用户输入（作答）

> I very like keep a pet, because it can make me not alone, but keep pet will cost many time, also dirty.

### AI 反馈

> **【我的原句】** I very like keep a pet, because it can make me not alone, but keep pet will cost many time, also dirty.
>
> **【优化句】** I **really enjoy keeping a pet**, because **it keeps me company**; however, **raising a pet takes much time** and may make the room messy.
>
> **【简短点评】** “I very like” 是副词位置的中文直译，“cost many time” 是中式搭配（花时间用 take，many 改 much）。立场清楚、有转折意识，补上 however 后逻辑更顺；建议再加一个小例子，表达会更饱满。
>
> 【继续】同一话题深度追问，开启新一轮作答
> 【重新回答】不换话题，重答本题，再次转写、优化、点评

### 用户回复【继续】后：AI 给出追问（AI 输出）

> **Topic:** Then do you think keeping pets teaches young people real responsibility?
> **Pro:** Feeding and walking a pet every day trains a young person to be reliable and caring.
> **Con:** Many teenagers only enjoy playing with pets while parents do the real routine work.

## 许可

本项目采用 MIT License，详见 [LICENSE](LICENSE)。

---

当前项目仅本地开发，未初始化 Git，未上传 GitHub。
