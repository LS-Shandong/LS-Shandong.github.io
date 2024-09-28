# 在 Wayland 环境下运行 Godot Engine

在 Wayland 环境下运行 Godot Engine。
&lt;!--more--&gt;
如题，我要在 Wayland 环境下运行官方仓库里的 Godot Engine。

方法如下：

复制 `/usr/share/applications/org.godotengine.Godot.desktop` 至 `$XDG_DATA_HOME/applications/`（例如 `~/.local/share/applications/`），文件内容如下：

```
[Desktop Entry]
Name=Godot Engine
GenericName=Libre game engine
GenericName[el]=Ελεύθερη μηχανή παιχνιδιού
GenericName[fr]=Moteur de jeu libre
GenericName[nl]=Libre game-engine
GenericName[zh_CN]=自由的游戏引擎
Comment=Multi-platform 2D and 3D game engine with a feature-rich editor
Comment[el]=2D και 3D μηχανή παιχνιδιού πολλαπλών πλατφορμών με επεξεργαστή πλούσιο σε χαρακτηριστικά
Comment[fr]=Moteur de jeu 2D et 3D multiplateforme avec un éditeur riche en fonctionnalités
Comment[nl]=Multi-platform 2D- en 3d-game-engine met een veelzijdige editor
Comment[zh_CN]=多平台 2D 和 3D 游戏引擎，带有功能丰富的编辑器
Exec=godot %f
Icon=godot
Terminal=false
PrefersNonDefaultGPU=true
Type=Application
MimeType=application/x-godot-project;
Categories=Development;IDE;
StartupWMClass=Godot

```
编辑如下一行：

```
...
Exec=godot --display-driver wayland %f
...

```

此方法仅适用于最新版本的 Godot Engine。


---

> 作者: LS-Shandong  
> URL: https://ls-shandong.github.io/posts/2024-9-08/  

