# 给 Tree 命令加上彩色输出

给 tree 命令加上彩色输出。
&lt;!--more--&gt;
默认安装的 Arch Linux 的 *ls* 命令是默认彩色输出的，而 *tree* 软件包提供的 tree  命令默认没有彩色输出。因为 Arch Linux 默认把 *ls* 设置为了 *ls --color=auto* 的别名，那么我们也采用这种方式。

打开 **~/.bashrc** ，插入以下一行：

`alias tree=&#39;tree -C&#39;`

然后注销再重新登录，此时再执行 tree 命令，就是彩色输出了。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-22-2/  

