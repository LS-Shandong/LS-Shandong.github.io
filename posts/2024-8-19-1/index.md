# 如何将 MIDI 音乐文件转换为 MP3 文件并压缩？

MIDI 曾经非常流行，。在专业音乐创作/编曲中，它仍然起着至关重要的作用。本文主要介绍将 MIDI（.mid）文件转换为 MP3 文件的方法。
&lt;!--more--&gt;

本文全部操作均在 Arch Linux 环境下。

## 需要的软件包

要转换 MIDI（.mid）文件，我们需要：

- 一个**常见的**合成器（比如 FluidSynth 或 TiMidty&#43;&#43;）

- soundfont（比如 Fluid 或 FreePats）

- 软件包 ffmpeg（TiMidty&#43;&#43; 需要） 或 twolame（FluidSynth 需要）

要压缩 MIDI（.mid）文件，我们需要：

- ffmpeg

上述软件包均存在于官方仓库中。要安装它们，直接运行：

`pacman -S 软件包名称`

## 转换

### 对于 FluidSynth

要将 MIDI（.mid）文件转换为 MP3 文件，运行：

`$ fluidsynth -l -T raw -F - /usr/share/soundfonts/FluidR3_GM.sf2 input.mid | twolame -b 256 -r - output.mp3`
{{&lt; admonition type=tip title=&#34;提示&#34; open=true &gt;}}
将 *FluidR3_GM.sf2* 替换为您选择的 *soundfont*，

将 *input.mid* 替换为要转换的 MIDI 文件，

将 *output.mp3* 替换为目标 mp3 文件。
{{&lt; /admonition &gt;}}


### 对于 TiMidty

要将 MIDI（.mid）文件转换为 MP3 文件，运行：

`$ timidity input.mid -Ow -o - | ffmpeg -i - -acodec libmp3lame -ab 256k out.mp3`

{{&lt; admonition type=tip title=&#34;提示&#34; open=true &gt;}}
将 *input.mid* 替换为要转换的 MIDI 文件，

将 *output.mp3* 替换为目标 mp3 文件。
{{&lt; /admonition &gt;}}

## 压缩

我们在前面转换的时候设置 mp3 文件码率为256kbps，可以通过降低码率来压缩 mp3，运行：

`$ ffmpeg -i input.mp3 -b:a 128k output.mp3`

{{&lt; admonition type=tip title=&#34;提示&#34; open=true &gt;}}
将 *input.mp3* 替换为要压缩的 mp3 文件，

将 *output.mp3* 替换为目标 mp3 文件。

将 *128k* 替换为目标码率
{{&lt; /admonition &gt;}}

还有其它方法，慢慢补充。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-19-1/  

