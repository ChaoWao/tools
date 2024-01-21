---
title: Shell
weight: 300
---
# Shell

## 常用命令

### 查看和更改 Shell 的常用命令

```sh
cat /etc/shells # 查看系统中支持的 Shell
echo $SHELL # 查看当前默认的 Shell
which your-shell # 查看 your-shell 所在的路径
chsh -s path-to-your-shell # 设置默认的 Shell
```

### 配置工作代理

当你需要配置工作代理时，可以使用如下命令：

```sh
export http_proxy=127.0.0.1:4780
export https_proxy=127.0.0.1:4780
```

为了更加便捷的使用，可以将如下代码加入到 rc 文件中。

```sh
# proxy management
proxy="127.0.0.1:4780"
function proxy_see {
    if [ -z "${http_proxy}" ] ; then
        echo "Your proxy for shell is off now!"
    else
        echo "Your proxy for shell is on now!"
    fi
}

function proxy_on {
    export http_proxy=${proxy}
    export https_proxy=${proxy}
    export HTTP_PROXY=${proxy}
    export HTTPS_PROXY=${proxy}
    echo "Your proxy for shell is on!"
}

function proxy_off {
    unset http_proxy
    unset https_proxy
    unset HTTP_PROXY
    unset HTTPS_PROXY
    echo "Your proxy for shell is off!"
}
```

## Bash: Bourne Again SHell

最通用的 Shell ，但是暂略。

## Zsh: Z shell

当前，也许你的系统中默认就使用 Zsh ，或提供了 Zsh 。如果没有，可以参考文章 [Installing ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) 完成 Zsh 的安装和配置。

如可以使用如下相应命令安装 Zsh ：

```sh
# install using apt
sudo apt install zsh
# install using pacman
sudo pacman -S zsh
```

### [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)

| 安装方法    | 安装命令                                                                                           |
| :-------- | :------------------------------------------------------------------------------------------------ |
| **curl**  | `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |
| **wget**  | `sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`   |
| **fetch** | `sh -c "$(fetch -o - https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |

### Configuration

Select the theme in `~/.zshrc`:

```
ZSH_THEME="eastwood"
```

### Extensions

#### aliases

```sh
plugins=(
    # other plugins...
    aliases
)
```

**Usage**

- `als`: show all aliases by group

- `als -h/--help`: print help message

- `als <keyword(s)>`: filter and highlight aliases by `<keyword>`

- `als -g <group>/--group <group>`: show only aliases for group `<group>`. Multiple uses of the flag show all groups

- `als --groups`: show only group names

#### colored-man-pages

```sh
plugins=(
    # other plugins...
    colored-man-pages
)
```

#### command-not-found

```sh
plugins=(
    # other plugins...
    command-not-found
)
```

#### extract

```sh
plugins=(
    # other plugins...
    extract
)
```

#### you-should-use

1. Clone this repository in oh-my-zsh's plugins directory:

    ```sh
    git clone https://github.com/MichaelAquilina/zsh-you-should-use.git $ZSH_CUSTOM/plugins/you-should-use
    ```

2. Activate the plugin in `~/.zshrc`:

    ```sh
    plugins=(
        # other plugins...
        you-should-use
    )
    ```

3. Configure by adding this line in `~/.zshrc`:

    ```sh
    export YSU_MESSAGE_POSITION="after"
    ```

4. Restart zsh (such as by opening a new instance of your terminal emulator).

#### zsh-syntax-highlighting

1. Clone this repository in oh-my-zsh's plugins directory:

    ```sh
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    ```

2. Activate the plugin in `~/.zshrc`:

    ```sh
    plugins=(
        # other plugins...
        zsh-syntax-highlighting
    )
    ```

3. Restart zsh (such as by opening a new instance of your terminal emulator).

#### zsh-autosuggestions

1. Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)

    ```sh
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    ```

2. Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):

    ```sh
    plugins=(
        # other plugins...
        zsh-autosuggestions
    )
    ```

3. Start a new terminal session.

#### zsh-autocomplete

1. Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)

    ```sh
    git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autocomplete
    ```

2. Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):

    ```sh
    plugins=(
        # other plugins...
        zsh-autocomplete
    )
    ```

3. Start a new terminal session.
