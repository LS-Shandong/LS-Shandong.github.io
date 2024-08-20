# 对 TTF 字体进行压缩与转换

在 HTML 网页里引用中文字体时，发现字体过大，导致加载得很慢。本文介绍了压缩与转换 ttf 字体的方法
&lt;!--more--&gt;
我在网络上查找了资料，基本上都说可以通过工具删去字体中不需要的部分，以达到压缩 ttf 字体的目的。

## 安装 font-spider

需要先安装 Node.js 和 npm（或 yarn），它们的安装和配置以后再说。

运行：

`# yarn global add font-spider`

## 压缩字体

### 准备工作

新建一个 HTML 文件，自定义要保留的字符，如下：

```HTML
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;meta charset=&#34;utf-8&#34;&gt;
    &lt;meta name=&#34;viewport&#34; content=&#34;width=device-width, initial-scale=1&#34;&gt;
    &lt;title&gt;&lt;/title&gt;
    &lt;style type=&#34;text/css&#34;&gt;
      @font-face {
        font-family: 字体名称;
        src: url(&#39;文件URL&#39;);
      }
      body {
        font-family: 字体名称;
      }
    &lt;/style&gt;
  &lt;/head&gt;
  &lt;body&gt;
  在这里写要保留的文字。可以直接把《义务教育语文课程常用字表》复制进来。
  &lt;/body&gt;
&lt;/html&gt;
```
![文件内容示例](images/blogs/2024-8-20-1/2024-8-20-1-1.jpg &#34;文件内容示例&#34;)

### 压缩字体

假设你编写的 HTML 文件叫作 *index.html*，运行：

`$ font-spider index.html`

![运行结果示例](images/blogs/2024-8-20-1/2024-8-20-1-2.jpg &#34;运行结果示例&#34;)

这样就把 32570.002 KB 大小的字体文件压缩到 3383.312 KB 了。

执行完后，它会把原来的字体文件移动到 .font-spider 文件夹,而原来的字体文件会被替换为压缩后的字体文件。如果有要补充的字符，把要补充的字符继续添加到 HTML 文件中，执行 `font-spider index.html` 即可。

## 转换字体

3 MB 多加载起来还是有点慢，我们可以把它转换成 woff2 格式。

在 Arch Linux 上，将 ttf 文件转换为 woff2 文件，需要安装软件包 *woff2*：

`# pacman -S woff2`

然后在字体所在目录，执行：

`$ woff2_compress 要转换的字体的名称`

![运行结果示例](images/blogs/2024-8-20-1/2024-8-20-1-3.png &#34;运行结果示例&#34;)

当前目录就会出现一个转换后的 woff2 文件。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-20-1/  

