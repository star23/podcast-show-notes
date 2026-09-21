# Podcast Show Notes

[English](#english) | [中文](#中文)

---

## English

Turn a podcast transcript into three drafts ready for further editing and publication: **a complete corrected transcript, show notes, and an edited highlights article**.

The skill first corrects speech-to-text errors using context and targeted web verification, then creates the other two documents from that corrected source. It is an instruction-based Agent skill that requires an existing transcript, not an executable transcription script or an audio-to-text service.

### Three outputs

1. **Corrected transcript**: Fix names, terminology, misheard words, punctuation, and sentence boundaries while preserving every speaking turn and original timestamp. Record material corrections and unresolved issues.

2. **Show notes**: An episode title built around a central question, an introduction, keywords, guest and host information, a topic timeline, and links to available transcripts or articles.

3. **Edited highlights article**: A standalone title, introduction, table of contents, thematic sections, and edited Q&A that preserves the stories and reasoning behind the ideas.

The timeline normally uses **one entry every 7–10 minutes**, grouping related material around actual topic transitions. Without timestamps, the skill provides a topic index rather than inventing times. Sparse timestamps are used as supplied, with that limitation noted. Uncertain words remain flagged. Potentially incorrect or outdated figures spoken by a guest are not silently replaced with newer numbers found online.

### Usage

Give the repository link to an Agent that can read and write files:

```text
Read SKILL.md and its referenced files at https://github.com/star23/podcast-show-notes,
then use the skill to edit my podcast transcript.
Transcript: /your/path/episode-80-transcript.md
Output directory: /your/path/episode-80-output
First save the complete corrected transcript, then create the show notes
and edited highlights article. Use English for the output and filenames.
```

You can also download the repository and ask the Agent to read the local `SKILL.md`. Keep the complete `references/` and `assets/` folders alongside it; the entry file alone is not the full skill.

#### Install in Codex

Clone the entire repository into your personal skills directory. Do not overwrite an existing destination:

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/star23/podcast-show-notes.git \
  "$HOME/.agents/skills/podcast-show-notes"
```

This is the personal skills location described in the [official Codex documentation](https://learn.chatgpt.com/docs/build-skills#where-to-save-skills). After installation, select `podcast-show-notes` in an interface that supports skill mentions, or ask the Agent to use it directly:

```text
Use $podcast-show-notes to process /your/path/episode-80-transcript.md.
Podcast: My Podcast
Episode: E80
Output directory: /your/path/episode-80-output
Use English for the output and filenames.
```

For other Agents, install the entire folder according to their skill-directory conventions, or use `SKILL.md` directly as the workflow for a task. The core workflow does not depend on Codex-specific tools; `agents/openai.yaml` contains optional interface metadata.

### Inputs, languages, and filenames

The skill accepts **Chinese or English transcripts and Chinese or English filenames**. Inputs may be local Markdown/TXT files, SRT/VTT subtitles, pasted text, or document links that the current environment can read in full. Optional details include the podcast name, episode number, participant bios, glossary, standard footer, language, length, and output directory. Missing metadata is not invented.

The output language follows the source transcript by default, and you can explicitly request another language. Section headings adapt to the output language. Your requested filenames and directory take priority. Example English output filenames:

```text
E80.transcript.corrected.md
E80.shownotes.md
E80.highlights.md
```

By default, the three Markdown files are saved next to the source transcript. The original is never overwritten. If output names already exist, the skill uses a consistent version suffix or a new directory. For document links or pasted text, the default destination is a topic subdirectory in the current working directory.

Generating drafts does not publish them automatically. Keep source transcripts and episode outputs in a separate content directory; this repository holds the reusable skill.

### Editorial reference

The editorial structure is drawn from the show notes and edited transcript of Day1Global E81, “Are You Benefiting from Large Models, or Being Absorbed by Them? AI Application Moats and Infrastructure Opportunities,” featuring Tang Liu of TiDB.

What carries over is the method: open with a concrete question, show the value of each timeline entry, and develop the reasoning through thematic sections and interview Q&A. Branding, contact details, guest identities, and episode-specific facts do not carry over to other podcasts. The repository contains a generalized style guide and reusable templates, not the full source interview.

### Repository structure

```text
SKILL.md
agents/openai.yaml
references/
  transcript-correction.md
  editorial-style.md
assets/
  corrected-transcript.template.md
  shownotes.template.md
  highlights.template.md
```

- `SKILL.md`: The skill entry point and complete workflow for all three outputs.
- `agents/openai.yaml`: Optional Codex interface metadata.
- `references/transcript-correction.md`: Rules for correction, verification, timestamps, and completeness.
- `references/editorial-style.md`: Editorial structure and style generalized from E81.
- `assets/`: Reusable Markdown templates for the three documents.

### Requirements

Use an Agent that can read the input and write files. The workflow uses the Agent’s search and web-reading tools when names, terms, or other details need verification. Without web access, it can still make context-supported corrections and identify what remains unverified. The repository itself requires no API key, dependency installation, or service deployment.

---

## 中文

把一份播客全文稿，变成三份可以继续编辑和发布的文稿：**完整修正版、Shownotes、精华稿**。

先结合上下文和必要的网络核验纠正语音转写错误，再从同一份底稿生成另外两份内容。这是一套指令型 Agent 技能，需要提供已有文字稿；它不是可执行的转录脚本，也不从音视频生成转写。

### 三份产出

1. **全文稿（修正版）**：纠正姓名、术语、误听与断句，保留全部发言和原时间戳，记录重要修正及疑点。

2. **Shownotes**：核心问题型标题、节目介绍、关键词、嘉宾主持、主题时间轴和已有文字稿入口。

3. **精华稿**：独立文章标题、导语、目录、主题分章与精编问答，保留故事和论证过程。

时间轴通常约每 **7–10 分钟一个节点**，按真实话题转折合并相关内容。没有时间戳时输出主题索引，不编分秒；原始标记稀疏时使用已有锚点并说明。不能确认的词保留并标记。嘉宾可能说错或过时的数据，不会仅凭最新搜索结果被悄悄改成另一个数字。

### 使用

可以把仓库链接交给有文件读写能力的 Agent：

```text
请读取 https://github.com/star23/podcast-show-notes 中的 SKILL.md 及其引用文件，
按这个技能处理我提供的播客全文稿。
全文稿：/你的目录/本期全文稿.md
输出目录：/你的目录/本期产出
先校订并保存完整修正版，再生成 Shownotes 和精华稿。
```

也可以先下载到本地，再让 Agent 读取本地 `SKILL.md`。完整保留 `references/` 和 `assets/`，不要只复制入口文件。

#### 在 Codex 中安装

将整个仓库克隆到个人技能目录；目标目录已存在时不要覆盖：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/star23/podcast-show-notes.git \
  "$HOME/.agents/skills/podcast-show-notes"
```

该目录是 [Codex 官方文档说明的个人技能位置](https://learn.chatgpt.com/docs/build-skills#where-to-save-skills)。安装后，在支持技能提及的界面中选择 `podcast-show-notes`，或直接让 Agent 使用它：

```text
使用 $podcast-show-notes，处理 /你的目录/E82. 全文稿.md。
节目名：我的播客
输出目录：/你的目录/E82-产出
```

其他 Agent 可按各自的技能目录约定安装整个文件夹，或直接将 `SKILL.md` 作为本次任务流程。核心工作流不依赖 Codex 特有工具；`agents/openai.yaml` 只是可选的界面元信息。

### 输入、语言与文件名

支持**中文或英文全文稿，以及中文或英文文件名**。输入可以是本地 Markdown/TXT、SRT/VTT、粘贴文本，或当前环境能够完整读取的文档链接。节目名、期号、人物介绍、术语表、品牌尾部、语言、篇幅和输出目录均可选；元信息缺失时不虚构。

输出语言默认跟随原稿，也可以明确指定另一种语言。栏目标题随输出语言调整；用户指定的文件名和目录优先。英文文件名示例：

```text
E80.transcript.corrected.md
E80.shownotes.md
E80.highlights.md
```

默认在原稿旁保存三个 Markdown 文件。原稿保持不变，遇到同名产出使用统一版本后缀或新目录。文档链接或粘贴文本默认输出到当前工作目录的主题子目录。

只生成文稿不会自动发布内容。全文稿及实际产出宜保存在独立的内容目录，仓库用于维护可复用的技能。

### 参考风格

编辑结构来自 Day1Global E81《你是大模型的受益方，还是被吞掉方？AI 应用的护城河与基础设施机会 ft. TiDB 唐刘》的 Shownotes 与精编文字稿。

保留的是编辑方法：介绍用具体问题切入，时间轴写出每段的价值，精编正文用主题章节和访谈问答展开推理。节目品牌、联系方式、嘉宾身份和本期事实不会自动继承到其他播客。仓库包含抽象后的风格说明与通用模板，不包含原始访谈全文。

### 仓库结构

```text
SKILL.md
agents/openai.yaml
references/
  transcript-correction.md
  editorial-style.md
assets/
  corrected-transcript.template.md
  shownotes.template.md
  highlights.template.md
```

- `SKILL.md`：技能入口，包含三份产出的完整流程。
- `agents/openai.yaml`：可选的 Codex 界面元信息。
- `references/transcript-correction.md`：纠错、核验、时间戳和完整性要求。
- `references/editorial-style.md`：从 E81 提炼的编辑结构与文风。
- `assets/`：三份可复用 Markdown 骨架。

### 运行条件

运行技能需要能读取输入并写入文件的 Agent；专名等有疑点时使用其搜索与网页阅读能力。无法联网时仍可完成上下文校订，并明确哪些项尚未核实。仓库本身无需 API Key、依赖安装或服务部署。
