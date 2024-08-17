# 在 Linux 上使用无线网卡（网卡基于RTL8188GU芯片）


&lt;!--more--&gt;

我的网卡为**迅捷150UH**，我准备在我的 Arch Linux 上使用之。

可运行 `lsusb` 命令以查询此网卡之芯片型号。lsusb 命令由软件包 `usbutils` 提供。

    $ lsusb

经查询，我的无线网卡芯片型号为 **RTL8188GU**，`linux-firmware`软件包中已包含驱动程序 `rtl8xxxu` ，这一般无需手动装载，要装载：

    # modprobe rtl8xxxu

但是，我的无线网卡基于 RTL8188GU，需要安装 `usb_modeswitch` 以将其切换至 Wifi 模式（这个网络上资料不多） 。

    # pacman -S usb_modeswitch

无线网卡已可使用。



---

> 作者: LS-Shandong  
> URL: ls-shandong.github.io/posts/2024-8-15-1/  

