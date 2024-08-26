# LaTeX 入门之软件安装

我新建了一个合集“$\LaTeX$ 入门”，主要记录我入门 $\LaTeX$ 的过程。本文主要记录使用 $\LaTeX$ 所需的软件的安装。本文在实际上代替了[这篇文章的作用](https://ls-shandong.github.io/posts/2024-8-17-1/)
&lt;!--more--&gt;
## 需要知道的信息
$\LaTeX$ 是一款流行的的排版系统，它基于 $\TeX$。要想使用 $\LaTeX$，我们需要一个 $\TeX$ 发行版和一个 $\TeX$ 编辑器。我选择了 $\TeX$ Live 发行版和 Kile 编辑器。

[$\TeX$ Live](https://www.tug.org/texlive/) 是一款流行的 $\TeX$ 发行版，它以年份作为发行版的版本号,保持一年一更的频率。一个 $\TeX$ 发行版是 $\TeX$ 排版引擎、支持排版的文件(基本格式、$\LaTeX$ 宏包、字体等)以
及一些辅助工具的集合。

[Kile](https://apps.kde.org/zh-cn/kile/) 是一款由 [KDE](https://kde.org/zh-cn/) 开发的 $\TeX$/$\LaTeX$ 编辑器。[Kile 官网](https://kile.sourceforge.io)。

## 安装

### 安装 $\TeX$ Live

在 [Arch Linux](https://archlinux.org) 安装 TeX Live 相当容易。有两种方法来安装 $\TeX$ Live。目前仅记录其中一种。

#### 安装官方仓库里打包的 $\TeX$ Live。

通过此方法安装 $\TeX$ Live 的好处是安装完成后开箱即用，无需设置环境变量。
[texlive](https://archlinux.org/groups/x86_64/texlive/) 包组包含大多数 $\TeX$ Live 包，根据上游集合进行分类。

[texlive-lang](https://archlinux.org/groups/x86_64/texlive-lang/) 包组包含为具有非拉丁字符的语言提供字符集和功能的包。一般来说，我们中国大陆的人安装 [texlive-langchinese](https://archlinux.org/groups/x86_64/texlive-langchinese/) 即可。

所以我们通过运行一条命令来安装 $\TeX$ Live：

`# pacman -S texlive texlive-langchinese`

{{&lt; admonition type=tip title=&#34;提示&#34; open=true &gt;}}
如果你缺少特定的 *.sty* 文件，你可以运行 `pacman -F` 来找到提供它们的 Arch 包。
{{&lt; /admonition &gt;}}

### 安装 Kile

运行以下命令以安装[官方仓库](https://archlinux.org/packages/extra/x86_64/kile/)里的 Kile：

`# pacman -S kile`




---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-26-1/  

