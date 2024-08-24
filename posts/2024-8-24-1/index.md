# Linux 启动时报错

每次开机都报错，最后排查出是网卡的问题。
&lt;!--more--&gt;
每次开机时都会报一堆错误，却不影响系统使用，这种情况从那次重装 Arch Linux 后就有了。

运行： `# journalctl -p err..alert` 得到结果是这样的（有删减）：

```
I/O error, dev sr1, sector 262128 op 0x0:(READ) flags 0x80700 phys_seg 1 prio class&gt;
I/O error, dev sr1, sector 262128 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 0
Buffer I/O error on dev sr1, logical block 32766, async page read
I/O error, dev sr1, sector 4096 op 0x0:(READ) flags 0x80700 phys_seg 1 prio class 0
I/O error, dev sr1, sector 4096 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 0
Buffer I/O error on dev sr1, logical block 512, async page read
I/O error, dev sr1, sector 260080 op 0x0:(READ) flags 0x80700 phys_seg 1 prio class&gt;
I/O error, dev sr1, sector 260080 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 0
Buffer I/O error on dev sr1, logical block 32510, async page read
Buffer I/O error on dev sr1, logical block 512, async page read
```

看报错好像是光盘驱动器坏了。我确实有一个光盘驱动器，但是它是正常的，而且，关键的是，我的光盘驱动器是 */dev/sr0* 而不是 */dev/sr1*。

运行 `ls /dev/` 发现 */dev/* 目录下只有 */dev/sr0*。

运行 `udevadm info /dev/sr1` ，得到 `Unknown device &#34;/dev/sr1&#34;: No such device`。

在 Arch Linux CN 的聊天群问了问，明白这是怎么回事了。

有些无线网卡厂家，为了实现“免驱”效果，会把网卡模拟成一个光驱，然后把驱动程序放入模拟光驱中，再放个 autorun 文件，网卡就会在首次插入 *Windows* 电脑时自动安装驱动程序。

然而它不会自动安装 Linux 驱动程序。在 Linux 上，驱动程序可作为内核模块（Module）使用。虽然 Linux 内核里包含了我的网卡的驱动程序，但是由于网卡还是会被识别为一个光驱，我们需要用软件 usb_modeswitch 来把它切换成 Wifi 模式。这便是我以前写的一篇文章[《在 Linux 上使用无线网卡（网卡基于 RTL8188GU 芯片）》](https://ls-shandong.github.io/posts/2024-8-15-1/)的主要内容。

显然,这个 */dev/sr1* 就是我的网卡，奇怪的是 /dev/sr0 和 /dev/sr1 都会启动时报 I/O 错误。您若是有什么见解可以在评论说出来。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-8-24-1/  

