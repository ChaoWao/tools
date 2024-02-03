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

`Linux` 修改配置文件：

```toml
import = ["~/.config/alacritty/dracula.toml"]

live_config_reload = true

[window]
opacity = 0.7
padding = { x = 10, y = 5 }
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

`Windows` 修改配置文件：

```toml
import = ["~\\AppData\\Roaming\\alacritty\\dracula.toml"]

shell = "C:\\Program Files\\PowerShell\\7\\pwsh.exe"

live_config_reload = true

[window]
opacity = 0.9
padding = { x = 10, y = 5 }
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

可以在 alacritty 的启动 shortcut 里把启动位置改为 `%USERPROFILE%` 。

## 全局唤出/隐藏功能

即类似 iTerm2 的 F12 的功能，可以在任意位置按下 F12 唤出/隐藏 iTerm2 。参考 [Request: Globbal toggle key](https://github.com/alacritty/alacritty/issues/862) 。

### Manjaro Xfce

参考 [Shell Script](https://github.com/alacritty/alacritty/issues/862#issuecomment-633320108) 。

```sh
mkdir -p ~/Apps/toggle-alacritty
touch ~/Apps/toggle-alacritty/toggle-alacritty.sh
chmod +x ~/Apps/toggle-alacritty/toggle-alacritty.sh
```

在 `toggle-alacritty.sh` 中填写：

```sh
#!/bin/bash

PID=$(pgrep alacritty)
if [ -z "$PID" ]; then
    alacritty &
    exit 0
fi

WINDOWID=$(xdotool search --pid $PID)
IS_VISIBLE=true
[ -z $(xdotool search --onlyvisible --pid $PID) ] && IS_VISIBLE=false

[ $(xdotool getwindowfocus) != "$WINDOWID" ] && {
    if [ $IS_VISIBLE == true ]; then
        xdotool windowactivate $WINDOWID
    else
        xdotool windowmap $WINDOWID
    fi

    exit 0
}

xdotool windowunmap $WINDOWID
```

在 Manjaro Xfce 中搜索 Keyboard ，随后在 Application Shortcuts 里新建一项。
- Command: `sh /your-home-path/Apps/toggle-alacritty/toggle-alacritty.sh`
- Shortcut: `CTRL+F12`

### Windows Terminal Quake

在 Windows 上可以借助 [flyingpie/windows-terminal-quake](https://github.com/flyingpie/windows-terminal-quake) 项目实现该功能。

目前该项目稳定版的 release 只支持 Windows Terminal 。但是 v2.0.0 的预览版支持所有应用，前提是要求该应用已经打开。

下载后添加

```json
{
    "HotKeys": [ { "Modifiers": "Control", "Key": "F12" } ],
    "StartNew": {
        // TODO: StartNew doesn't work yet.
        "FileName": "C:/Program Files/Alacritty/alacritty.exe"
    },
    "FindExisting": {
        "ProcessName": "alacritty"
    }
}
```
