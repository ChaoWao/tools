---
title: 版本控制工具
weight: 310
---
# 版本控制工具

## [Git](https://git-scm.com/)

### 为 Git 配置工作代理

Git 有两种工作模式，分别是 https 工作模式和 ssh 工作模式。
如在下载[该仓库](https://github.com/ChaoWao/tools)时， github 给出的两个选项：

```sh
git clone https://github.com/ChaoWao/tools.git
git clone git@github.com:ChaoWao/tools.git
```

因此，当你需要为 Git 配置工作代理时，首先要区分你正在使用哪种工作模式。

### 为 Git/https 配置工作代理

为 https 工作模式的 Git 配置代理，可以使用如下命令：

```sh
git config --global http.proxy http://127.0.0.1:4780
git config --global https.proxy http://127.0.0.1:4780
```

为了更加便捷的使用，可以将如下代码加入到 rc 文件中。

```sh
# git proxy management
function git_proxy_see {
    git_proxy=$(git config --global --get http.proxy)
    if [ -z "${git_proxy}" ] ; then
        echo "Your proxy for git is off now!"
    else
        echo "Your proxy fot git is on now!"
    fi
}

function git_proxy_on {
    git config --global http.proxy http://127.0.0.1:4780
    git config --global https.proxy http://127.0.0.1:4780
    echo "Your proxy for git is on!"
}

function proxy_off {
    git config --global --unset http.proxy
    git config --global --unset https.proxy
    echo "Your proxy for git is off!"
}
```

### 为 Git/ssh 配置工作代理

为 ssh 工作模式的 Git 配置代理，需要在 `~/.ssh/config` 文件中配置。有走 socks 和走 https 两个设置方案。以 github 为例，走 HTTP 代理需要添加：

```sh
Host github.com
    User git
    HostName ssh.github.com
    Port 443
    ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=4780
```

走 socks5 代理需要添加

```sh
Host github.com
    User git
    HostName ssh.github.com
    Port 443
    ProxyCommand nc -v -x 127.0.0.1:4780 %h %p
```

可能需要安装依赖：

```sh
# 使用 pacman 安装 socat
sudo pacman -S socat
# 使用 pacman 安装 nc
sudo pacman -S openbsd-netcat
```

至于为什么 github 要设置一个奇怪的端口号 443 ，而不是使用 ssh 默认的端口号 22 ，可以参考文章 [Using SSH over the HTTPS port](https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)
