# Lany Typography Prompts

为封面、主页横幅、卡片和正文配图编写中文标题的字形与字效提示词。你给出逐字文案、尺寸与用途，技能明确笔画、字面、间距、配色和安全区；也可以在宿主支持时生成文字图。

默认使用克制的几何无衬线。像素人物并不要求配像素标题；正文写作和整张封面构图由各自的工作流负责。

## 安装与更新

需要能读取本地 Skill 的 Agent；以下为 Codex 本地安装示例。仓库名带 `-skill`，实际调用名为 `$lany-typography-prompts`。

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/LanyXiaosheng/lany-typography-prompts-skill.git ~/.agents/skills/lany-typography-prompts
```

按照 [Codex 官方技能文档](https://learn.chatgpt.com/docs/build-skills)，用户级技能目录为 `~/.agents/skills/`，项目级可放在 `.agents/skills/`。安装后应自动发现；未显示时重启 Codex。若已有 `~/.codex/skills/lany-typography-prompts` 且当前客户端能够加载，请沿用该副本，避免重复安装同名技能。其他 Agent 按其技能目录规则放入完整仓库，并让它读取 `SKILL.md`。

更新前先检查本地修改；有修改时先提交或备份，再拉取。以下路径要与实际安装位置一致：

```sh
git -C ~/.agents/skills/lany-typography-prompts status --short
git -C ~/.agents/skills/lany-typography-prompts pull --ff-only
```

仓库包含工作流和资源，不自带生图服务或模型凭据。只读方案/提示词可以直接使用；实际生图取决于宿主已提供的图片生成能力。

## 快速调用

### 只生成提示词

```text
使用 $lany-typography-prompts，为封面标题编写可直接用于生图的提示词，暂时不出图。
主标题逐字为“把想法做成作品”，副标题为“从一次小实验开始”。
用途：16:9封面中的文字模块。
背景：#0A0A0A；主字暖白，#D8FF00只用于一处强调。
标题最多两行，左侧排字，右侧留给人物。
保留完整封面中已经确认的其他文案，不额外限制整幅图只能出现这些字。
```

### 生成独立文字图

```text
使用 $lany-typography-prompts，生成一张1600×900独立文字图。
主标题逐字为“今天，开始交付。”，无副标题。
黑底暖白字，一条 #D8FF00 短下划线，不加其他字。
先确定字形与排版，再出图；逐字核对标点和字序。
若生图文字错误，用可编辑文字重排，并保存源文件与正式PNG。
项目目录为当前项目，slug 使用 start-shipping。
```

### 配合 Banner

```text
使用 $lany-typography-prompts，为已确认的Banner布局设计“Lany 小生”的名称字形。
继承Banner的配色、标题位置与头像安全区，只调整这组文字。
给出一种主方向和一种可选字效，并说明小尺寸下的可读性。
```

## 输入与工作方式

| 输入 | 必要信息 |
| --- | --- |
| 逐字文案 | 主标题、副标题或明确写“无”，保留原标点 |
| 用途 | 独立文字图，或封面/Banner内嵌文字模块 |
| 画幅与位置 | 像素尺寸或比例、文字区域、需要留空的位置 |
| 背景与颜色 | 独立使用时指定；嵌入其他资产时继承其已确认规则 |
| 交付形式 | 仅提示词，或提示词＋正式图片＋必要的可编辑源文件 |

每张图保留一种字形主方向和至多一种字效。先写清文字，再决定笔画粗细、宽窄、字距、材质与层级。只有文章没有标题时，先提出待确认文案。

## 输出文件

仅在对话中请求提示词时直接返回文本；作为项目资产时保存到：

```text
lany-assets/lany-typography-prompts/start-shipping/
├── prompts/type.md
├── type-source.png     # 请求并成功生成图片时
├── type.png            # 校准后的正式图
└── type.svg 或 type.html  # 使用可编辑文字修正时
```

同名文件使用版本后缀。项目根优先采用你指定的位置，其次为明确文章的所在目录，最后才是当前可写工作目录。

## 验收与常见问题

- **生图出现乱码或错字：** 提示词不能保证文字正确。逐字校对后，用真实字体在 SVG/HTML 或设计文件中重排并重新导出。
- **效果很好但缩小后看不清：** 减少纹理、发光和字效，拉开层级，检查手机缩图及标题安全区。
- **没有生图工具：** 仍可生成完整提示词；实际图片需要宿主工具支持。
- **能否指定字体：** 可以，但应确认环境已安装该字体，并核对实际素材许可；没有安装的字体不能报告为已使用。
- **会不会改完整封面：** 内嵌模式只处理指定文字模块，人物、背景和其他文案遵循父任务的规则。
- **调用找不到：** 使用 `$lany-typography-prompts`，仓库名末尾的 `-skill` 不属于调用名。

相关工作流：[封面](https://github.com/LanyXiaosheng/lany-cover-skill)、[Banner](https://github.com/LanyXiaosheng/lany-banner-skill)。

## 仓库导航

- [SKILL.md](SKILL.md)：完整执行规则。
- [agents/openai.yaml](agents/openai.yaml)：技能展示信息。
- [品牌字形规则](references/brand-type.md)：默认方向与文字层级。
- [提示词结构](references/prompt-blueprint.md)：独立字图与内嵌模块的写法。
- [DESIGN.md](DESIGN.md)：拆分设计与边界。

来源：[lany-skills/lany-typography-prompts](https://github.com/LanyXiaosheng/lany-skills/tree/master/lany-typography-prompts)。本仓库独立安装，调用名保持 `lany-typography-prompts`。
