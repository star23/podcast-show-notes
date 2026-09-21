# Podcast Show Notes

把一份播客全文稿，变成三份可以继续编辑和发布的文稿：**完整修正版、Shownotes、精华稿**。

先结合上下文和必要的网络核验纠正语音转写错误，再从同一份底稿生成另外两份内容。它是一套 Agent 编辑技能，不是自动转录程序；需要提供已有文字稿。

## 三份产出

| 产出 | 做什么 |
| --- | --- |
| 全文稿（修正版） | 纠正姓名、术语、误听与断句，保留全部发言和原时间戳，记录重要修正及疑点 |
| Shownotes | 核心问题型标题、节目介绍、关键词、嘉宾主持、主题时间轴和已有文字稿入口 |
| 精华稿 | 独立文章标题、导语、目录、主题分章与精编问答，保留故事和论证过程 |

时间轴通常约每 **7–10 分钟一个节点**，按真实话题转折合并相关内容。没有时间戳时输出主题索引，不编分秒；原始标记稀疏时使用已有锚点并说明。不能确认的词保留并标记。嘉宾可能说错或过时的数据，不会仅凭最新搜索结果被悄悄改成另一个数字。

## 使用

可以把仓库链接交给有文件读写能力的 Agent：

```text
请读取 https://github.com/star23/podcast-show-notes 中的 SKILL.md 及其引用文件，
按这个技能处理我提供的播客全文稿。
全文稿：/你的目录/本期全文稿.md
输出目录：/你的目录/本期产出
先校订并保存完整修正版，再生成 Shownotes 和精华稿。
```

也可以先下载到本地，再让 Agent 读取本地 `SKILL.md`。完整保留 `references/` 和 `assets/`，不要只复制入口文件。

### 在 Codex 中安装

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

## 输入选项

支持本地 Markdown/TXT、SRT/VTT、粘贴文本和当前环境能够完整读取的文档链接。节目名、期号、人物介绍、术语表、品牌尾部、语言、篇幅和输出目录均可选。默认沿用原稿语言和信息；元信息缺失时不虚构。

默认在原稿旁保存三个 Markdown 文件。原稿保持不变，遇到同名产出使用统一版本后缀或新目录。文档链接或粘贴文本默认输出到当前工作目录的主题子目录。

只生成文稿不会自动发布内容。全文稿及实际产出宜保存在独立的内容目录，仓库用于维护可复用的技能。

## 参考风格

编辑结构来自 Day1Global E81《你是大模型的受益方，还是被吞掉方？AI 应用的护城河与基础设施机会 ft. TiDB 唐刘》的 Shownotes 与精编文字稿。

保留的是编辑方法：介绍用具体问题切入，时间轴写出每段的价值，精编正文用主题章节和访谈问答展开推理。节目品牌、联系方式、嘉宾身份和本期事实不会自动继承到其他播客。仓库包含抽象后的风格说明与通用模板，不包含原始访谈全文。

## 仓库结构

```text
SKILL.md                              技能入口和三份产出的完整流程
agents/openai.yaml                    Codex 界面元信息
references/transcript-correction.md    纠错、核验、时间戳和完整性要求
references/editorial-style.md          从 E81 提炼的编辑结构与文风
assets/corrected-transcript.template.md
assets/shownotes.template.md
assets/highlights.template.md          三份可复用 Markdown 骨架
```

运行技能需要能读取输入并写入文件的 Agent；专名等有疑点时使用其搜索与网页阅读能力。无法联网时仍可完成上下文校订，并明确哪些项尚未核实。仓库本身无需 API Key、依赖安装或服务部署。
