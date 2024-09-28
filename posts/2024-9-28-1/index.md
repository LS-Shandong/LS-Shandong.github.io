# 使用 Timeshift 备份系统

BTRFS 是一种现代的写时复制（COW）Linux 文件系统，Timeshift 可帮助定期创建文件系统的增量快照。
&lt;!--more--&gt;
---
&gt; 摘自 Arch Linux 中文维基：
&gt;
&gt;*Timeshift* 可帮助定期创建文件系统的增量快照，然后在以后恢复到这些快照，以撤销对系统的所有更改。

本文主要介绍 Timeshift 在 Arch Linux 上的配置（使用 Btrfs 文件系统的快照功能），仅供参考。

## 需要安装的软件包

安装 `Timeshift` 软件包以获得 *Timeshift* 本体。

可选：安装 `grub-btrfs` 软件包以在每次生成 GRUB 配置时向 GRUB 菜单添加快照。

安装 `btrfs-progs` 以获得 Btrfs 分区基础操作所必须的工具。

## Timeshift 配置
### 需要的分区配置
*Timeshift* 需要驱动器 */* 目录和 */home* 目录分别使用 *@* 和 *@home* 子卷布局配置。

所以我安装 Arch Linux 的时候是像这样分区的[仅针对根分区(/dev/sda6)]：

```bash
# 格式化并挂载分区
mkfs.btrfs /dev/sda6
mount /dev/sda6 /mnt
# 创建普通的子卷
btrfs subvolume create /mnt/@
btrfs subvolume create /mnt/@home
btrfs subvolume create /mnt/@log
btrfs subvolume create /mnt/@pkg
# 创建 swap 子卷及 swap 文件
btrfs subvolume create /mnt/swap
btrfs filesystem mkswapfile --size 8g --uuid clear /mnt/swap/swapfile
# 启用 swap 文件
swapon /mnt/swap/swapfile
# 卸载分区
umount /dev/sda6
# 挂载分区(noatime、discard=async 与 compress=zstd 是可选的)
mount /dev/sda6 /mnt -o subvol=@,noatime,discard=async,compress=zstd
# 新建目录
mkdir /mnt/home
mkdir -p /mnt/var/log
mkdir -p /mnt/var/cache/pacman/pkg
# 挂载子卷(noatime、discard=async 与 compress=zstd 是可选的)
## 挂载 /home 目录
mount /dev/sda6 /mnt/home -o subvol=@home,noatime,discard=async,compress=zstd
## 挂载 /var/log 目录
mount /dev/sda6 /mnt/var/log -o subvol=@log,noatime,discard=async,compress=zstd
## 挂载 /var/cache/pacman/pkg 目录
mount /dev/sda6 /mnt/var/cache/pacman/pkg -o subvol=@pkg,noatime,discard=async,compress=zstd
# 因为我不希望 /var/log 和 /var/cache/pacman/pkg 在将来被保存快照，所以选择为这两个目录禁用写时复制：
chattr &#43;C /mnt/var/log
chattr &#43;C /mnt/var/cache/pacman/pkg
# 生成 fstab 文件
genfstab -U /mnt &gt;&gt; /mnt/etc/fstab
```
### 软件配置

按照向导设置，记得要启用 cronie 服务：

    # systemctl enable cronie.service --now

`grub-btrfs` 软件包附带 `grub-btrfsd.service`，启用后可在创建新快照时自动更新 GRUB 配置。

要使 `grub-btrfsd` 与 `Timeshift` 一起工作，请运行以下命令编辑服务：

    # systemctl edit --full grub-btrfsd

并将 `grub-btrfsd --syslog /.snapshots` 替换为 `grub-btrfsd --syslog -t`。 这样 grub-btrfs 就会监视 Timeshift 创建的快照。
## Timeshift 的 man 手册页翻译

还没有开始……

---
本文写得匆忙，有疏漏之处请指出。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-9-28-1/  

