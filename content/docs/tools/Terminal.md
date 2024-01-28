---
title: 终端
weight: 200
---
# 终端

## Alacritty

[官网](https://alacritty.org/index.html)

### 安装

```sh
# Manjaro
pamac install alacritty
```

### 配置

配置文件路径：

- Windows: `%APPDATA%\alacritty\alacritty.toml`
- Linux: `$HOME/.config/alacritty/alacritty.toml`

下载 Dracula 配色：

```sh
# Linux
wget -O- https://raw.githubusercontent.com/dracula/alacritty/master/dracula.toml ~/.config/alacritty/dracula.toml
```

修改配置文件：

```toml
import = ["~/.config/alacritty/dracula.toml"]

live_config_reload = true

[window]
opacity = 0.7
dynamic_padding = false
startup_mode = "Maximized"
decorations = "None"

[scrolling]
history = 2000
multiplier = 20

[font]
normal = { family = "MesloLGS NF", style = "Regular" }
bold = { family = "MesloLGS NF", style = "Bold" }
italic = { family = "MesloLGS NF", style = "Italic" }
bold_italic = { family = "MesloLGS NF", style = "Bold Italic" }
size = 16
```
