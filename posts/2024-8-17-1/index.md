# Arch Linux 上 LaTex 环境的安装与配置

我们要使用 Latex,一般是要安装 Tex Live 和一个 Latex 编辑器，这在 Linux 上很容易实现。
&lt;!--more--&gt;

## 安装

## 安装 Tex Live

TeX Live 包括许多 Tex 引擎，如 pdfTex、XeTex、LuaTex。

官方仓库里存在一个名为 **texlive** 的软件包组，其中包含了包含大多数 TeX Live 包，根据上游集合进行分类，还要安装 **texlive-lang** 以获得中文等语言的支持。

此外，还可以安装 **texlive-doc** 以获得整个 TeX Live 文档和源文件。

## 安装编辑器

我个人比较倾向于使用 **TeXstudio** 和 **kile**。直接从官方源安装即可。

### TeXstudio 的配置

要启用 XeTex 以获得 Unicode 和现代字体技术支持,转至 ***选项 &gt; 设置TeXstudio &gt; 构建 &gt; 默认编译器***。选择 *XeTex* 即可。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-17-1/  

