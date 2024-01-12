# 浙江大学学位论文 LaTeX 模板

[![ZJUTHESIS](https://img.shields.io/badge/zjuthesis-latex-blue.svg)](https://thenetadmin.github.io/zjuthesis)
[![GitHub release](https://img.shields.io/github/release/TheNetAdmin/zjuthesis.svg?label=version&style=popout)](https://github.com/TheNetAdmin/zjuthesis/releases/latest)
[![GitHub All Releases](https://img.shields.io/github/downloads/thenetadmin/zjuthesis/total.svg?color=blue&style=popout)](https://github.com/TheNetAdmin/zjuthesis/releases/latest)
[![Commit Since Latest Release](https://img.shields.io/github/commits-since/TheNetAdmin/zjuthesis/latest.svg)](https://github.com/TheNetAdmin/zjuthesis/commits/master)
[![GithubAction](https://github.com/TheNetAdmin/zjuthesis/workflows/Build%20Tests/badge.svg)](https://github.com/TheNetAdmin/zjuthesis/actions)
[![GitHub Discussion](https://img.shields.io/badge/github-discussion-blue)](https://github.com/TheNetAdmin/zjuthesis/discussions)

## 简介

本项目为浙江大学学位论文的 LaTeX 模板，包含本科生、硕士生与博士生模板，以及英文硕博士模板。

This is a LaTeX template for Zhejiang University graduation thesis/design.
It provides undergraduate and graduate (master and doctor) templates.
It also provides an English template for graduate students.
See [English template user manual](./docs/english.md) for more details.

[CC98 校内讨论贴](https://www.cc98.org/topic/4762356)

[GitHub 讨论版](https://github.com/TheNetAdmin/zjuthesis/discussions)

## 个性化修改

当无助的毕业生因学院的word模板发愁时，zjuthesis说latex，于是世界有了光

### packages

添加`amsmath`，`amsthm`和`cleveref`环境。`cleveref`环境置于最后。

我真的很需要`align`和`<environment>*`环境，虽然不再latex-core里面，但`amsmath`的使用也相当广泛了，我不理解原库为啥不用。

`amsthm`和`cleveref`包，因为需要`lemma`环境且引用`lemma`环境得到`引理 *.*`，还要和`theorem`公用计数器，我查了很多方法，`hyperref`只能从零自定义，嫌麻烦直接用现成包。`lemma 1`作为整体超链接而非仅仅`1`。

后续还可以添加`definition,proposition,formula,exercise,notation,note,remark,example,corollary`环境，不过这些写论文用不到，做笔记很有用。

### command

添加`theorem`，`lemma`环境。二者公用计数器`theorem`，该计数器随`section`重置为零。二者也可以不共用计数器，但是相信我，共用是最好的。

重定义`amsthm`自带`proof`环境，使**证明**粗体。

### numbering

公式编号从`*-*`修改为`*.*`。理由是当引用多个公式时显示`(1-1)-(1-4)`很丑(编译出的结果`-`很长且两边有空格)。为了避免定理等格式产生冲突。引用公式时使用`eqref`，引用定理等使用`cref`，这保证`(*.*)`一定代表公式。引用公式较多时，使用`autoref`会得到大量`式 *.*`，不美观且十分啰嗦。

### translation

本科毕业设计默认使用`chaptermajornumbeing`，这导致外文翻译时编号按照chapter而非论文自身的`section`(论文通常用不到chapter吧...)，所以在translate文件中使用`\sectionmajornumbering`，来保证翻译与原文编号的一致。这样的好处就是不用大量`\label`和`\ref`，因为你保证了编号一致，直接用编号就行了，虽然很蠢...但是能省很多时间，缺点就是编号没有超链接。

## 使用

zjuthesis 模板有三种使用方式，Overleaf，本地编译，或者 Container 编译：

- Overleaf 是一个线上 LaTeX 编辑器，可以在不安装任何工具的情况下编写 LaTeX 文档，同时也可以和其他人共享文档，共同编辑。
- 本地编译比 Overleaf 更快，而且本地编译可以使用 Git 来记录版本。推荐有能力的同学设置本地编译环境，并推荐使用 Visual Studio Code 配合 LaTeX workshop 插件 (vscode 使用方式见[FAQ](./docs/FAQ.md))。
- Container 编译是使用 GitHub 提供的 Codespace 搭配 Container 来编译，这个环境提供了浏览器内的 VS Code 界面以及 TeX Live 的编译环境。这种方式适合熟悉 Container 与 GitHub Codespace 相关用法的同学使用。

### Overleaf

1. [下载模板代码](https://github.com/TheNetAdmin/zjuthesis/releases) 中的 `zjuthesis-v*.*.*-overleaf.zip` 文件
1. 在 Overleaf 中上传这个 .zip 压缩文件以创建一个新 Overleaf 项目
1. 在 Overleaf 界面左上角点击 "Menu"
   - 选择 "Compiler" 为 "XeLaTeX"
   - 选择 "TeX Live version" 为 "2019" 或者更新的版本
1. 参照 Overleaf 项目中 `fonts/README.md` 的说明下载所需字体，并上传到 `fonts` 文件夹中
1. 使用 Overleaf 编译
   - 选择专业模板与毕业学位的方式参见下文 "本地编译"

### 本地编译

1. 安装 TeXLive 工具包，编译需要 XeTeX 引擎。安装过程可以参考[浙江大学镜像站提供的文档](https://mirrors.zju.edu.cn/docs/CTAN)，以便在校内网下更快下载。
1. [下载模板代码](https://github.com/TheNetAdmin/zjuthesis/releases)，
   每个专业模板都有预览 pdf 文件，可以单独下载查看。
   模板代码请下载 `zjuthesis-v*.*.*.zip` 文件
   （如果你在用 Clone 或者 Fork 得到的代码，请切换到最新的 release tag，避免 master 分支上的不稳定更新破环你的论文的样式）
1. 在 `zjuthesis.tex` 中 `\documentclass[]{zjuthesis}` 部分填写个人信息，其中以下信息用于控制文档的生成：

   - `Degree` 为 `undergraduate` 时，编译本科生论文：

   | Field       | Option 1                             | Option 2                               | Option 3                           |
   | :---------- | :----------------------------------- | :------------------------------------- | :--------------------------------- |
   | Type        | thesis: 论文类                       | design: 设计类                         |                                    |
   | Period      | proposal: 开题报告                   | final: 最终论文/设计（含开题报告）     | paper: 最终论文/报告（无开题报告） |
   | BlindReview | true: 生成盲审用 pdf（隐藏个人信息） | false: 生成提交用 pdf                  |                                    |
   | MajorFormat | general: 默认模板                    | 与 `config/format/major/` 下目录名相同 |                                    |

   - `Degree` 为 `graduate` 时，编译硕士生/博士生论文：


   | Field       | Option 1                             | Option 2                               |
   | :---------- | :----------------------------------- | :------------------------------------- |
   | Type        | thesis: 学术论文                     | design: 专业学术论文                   |
   | BlindReview | true: 生成盲审用 pdf（隐藏个人信息） | false: 生成提交用 pdf                  |
   | MajorFormat | general: 默认模板                    | 与 `config/format/major/` 下目录名相同 |
   | GradLevel   | master: 硕士                         | doctor: 博士                           |

   - 其他设置

   | Field         | Option 1                                  | Option 2            |
   | :------------ | :---------------------------------------- | :------------------ |
   | PrintFilePath | true: 在每页侧边打印该页对应 TeX 文件路径 | false: 不打印此输出 |
   | TwoSide       | true: 章节末的偶数页留白，保证下章节的标题位于奇数页 | false: 取消偶数页留白 |

1. 在 `body` 目录下编写内容
1. 在 `pages` 目录下填写必要的内容，如审核评语等
1. 在 `figure` 目录下保存图片，在 `body/ref.bib` 内插入文献条目
1. 在根目录下运行命令 `latexmk`（或者 `latexmk -xelatex -outdir=out zjuthesis`）即可使用 XeTeX 编译 pdf 文件到 `out` 目录（该目录不会被记录版本）。**请务必使用此 `latexmk` 命令进行编译（除非你已经了解 LaTeX 的工作机制），否则你可能遇到参考文献无法显示等问题**
1. 如需使用 LuaTeX 编译，可运行命令 `latexmk -pdflua -outdir=out`

> **注意**
>
> - 每年的三月底四月初会有 TeXLive 的版本升级，届时本模板会根据 TeXLive 的更新做出一定的修改，请在提交最终论文前查看并应用本模板的更新。
> - 如果你使用 Mac OS 10.15 及以上版本，并且 TexLive 中的 ctex 包版本低于 2.5，会产生[宋体字体判断问题](https://github.com/TheNetAdmin/zjuthesis/issues/79)，导致编译得到的 pdf 中字体出现误差。要解决这个问题，可以将 ctex 包升级到 2.5 以上，或者临时在 ctex 包的选项中加入 `fontset=macnew`，详见 [issue  79](https://github.com/TheNetAdmin/zjuthesis/issues/79)。
> - 本模板已经兼容 TeXLive 2021。TeXLive 2018 以及之前的版本复制伪粗体文字会产生乱码，建议使用本地 TeXLive 的同学使用最新版 TeXLive。
> - 计算机专业的部分页面与学校通用格式不同，如果你是计算机专业的同学，请使用计算机专业的模板。

### 使用容器编译

本模板提供了一套配置文件，用以支持在容器中安装TeX Live，项目使用的字体，以及VS Code上的[LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)插件，配合GitHub Codespaces可以做到开箱即用。感谢 [FUTURETECH6](https://github.com/FUTURETECH6) 同学贡献的[代码](https://github.com/TheNetAdmin/zjuthesis/pull/222)。

GitHub Codespace使用方法：

1. 创建个人的项目（直接fork，或自行clone并修改remote）
1. 在个人的项目主页点击"Code"
1. 点击"Codespaces"
1. 点击"New codespace"
1. 等待容器构建（这一过程约要10分钟，因为要在标准Ubuntu的镜像中安装TeX Live）
1. 构建完成后，可以选择在VS Code（需要[GitHub Codespaces](https://marketplace.visualstudio.com/items?itemName=GitHub.codespaces)插件）中或在浏览器中打开，然后按照在本地的使用方式使用

> **注意**
>
> - 这一功能的初衷是为了方便性能较弱的设备（例如低功耗笔记本电脑）也能利用免费的云运算资源较快地完成编译，因此**不建议**在本地性能较强的机器上使用（请改用"本地编译"）。

### 字数统计

本模板提供了一个脚本用于统计正文字数，请在根目录下使用 `latexmk` 编译一遍模板，然后执行脚本 `script/utils/word_count.sh`。
此脚本调用了 `texcount` 工具，该工具是 TeX Live 的一部分，不需要额外安装。

## Slides 模板

作者用于毕业答辩的一个 Slides 模板 (Microsoft PowerPoint 模板)

- [GitHub 下载链接](https://github.com/TheNetAdmin/zjuthesis/releases/tag/v2.1.1-slide)
- [Gitee （国内镜像仓库）下载链接](https://gitee.com/netadmin/zjuthesis/releases/v2.1.1-slide) 国内网络用这个链接下载比较快

[HGGshiwo](https://github.com/HGGshiwo) 同学于 2021 年开发了基于 Beamer 的 Slides 模板，有兴趣的同学可以参考如下几个 repo

- [Formal](https://github.com/HGGshiwo/BeamerthemeFormal) (内含对其他几个 Beamer 模板的简介)
- [Brief](https://github.com/HGGshiwo/BeamerthemeBrief)
- [Mixture](https://github.com/HGGshiwo/BeamerthemeMixture)
- [Classical](https://github.com/HGGshiwo/BeamerthemeClassical)

## 参考文档

常见问题与解决方案请参考[FAQ](./docs/FAQ.md)，模板使用请参考[使用手册](./docs/usage.md)，模板修改与二次开发请参考[开发手册](./docs/develop.md)。

本模板所使用的各专业规范文件请参考 [zjuthesis-std](https://github.com/thenetadmin/zjuthesis-std)。

## 贡献

对本项目最好的贡献方式是在 GitHub Issue 里提交你发现的 BUG，或者贡献 Pull Request。
如果你不熟悉 GitHub 的运作方式，也可以通过邮件联系我，联系方式位于 `zjuthesis.tex` 顶部。

本项目提供了 LaTeX 模板，但并不负责教会用户使用各种 LaTeX 工具与环境。
与工具和环境有关的问题（例如 TeXStudio 如何处理参考文献）请先自行上网搜索解决方案。
在本项目的 GitHub Issue 里也已经有很多相关内容可供查阅。
当以上尝试均失败后，可到本项目的 [GitHub Discussion](https://github.com/TheNetAdmin/zjuthesis/discussions) 板块进行讨论。

本项目的 Issue 板块只处理使用命令行 `latexmk` 命令编译后产生的问题，不处理使用其他工具（如 TeXStudio）产生的问题。

## 开源许可

本项目代码基于 MIT 协议开源

学校标志与学校文件的版权归浙江大学所有
