# wsl2proxy

让 wsl2 "透明"使用 windows 中的代理

## 安装

```shellscript
# 在 linux 子系统下执行
cd /usr/local && sudo git clone https://github.com/akirarika/wsl2proxy.git && cd wsl2proxy && sudo chmod +x ./wsl2proxy
```

接着在你使用的 shell 配置文件**末尾**添加 *(例：使用 `bash` 则在 `~/.bashrc`，`zsh` 在 `~/.zshrc`)*

```shellscript
# 向脚本传递两个参数，以指定你在 windows 下代理程序的协议和端口
# source /usr/local/wsl2proxy/wsl2proxy [协议] [端口]
source /usr/local/wsl2proxy/wsl2proxy socks5 7891
```

配置好后重启终端即可。

重启后输入 `proxy "curl https://www.google.com/"` 查看是否成功了吧！

你甚至可以 `proxy bash` 直接打开被透明代理的一个 shell

如果希望启动后直接打开经过透明代理的 shell，可继续在末尾添加：

```shellscript
# 避免递归打开的问题
if [ ! $IS_ROOT_SHELL ];then
    proxy bash
    exit
fi
```

## 使用

### 启动使用透明代理的 shell 或程序

```shellscript
# proxy [命令]
proxy bash
proxy "curl https://www.google.com/"
```

## 常见问题

### 安装 proxychains 时报错 "cannot find an option to set library name"

详见这个 [issue](https://github.com/rofl0r/proxychains-ng/issues/234)

### 端口号和协议配置的正确了，为什么还是连不上？

要在你的代理程序中允许来自局域网的请求，如打开 `Allow LAN` 开关，或将服务监听地址从 `127.0.0.1` 改为 `0.0.0.0` 等，根据你使用的客户端而异

如果开启后依然无效，可重启电脑再试

### 协议类型可以填哪些？

http，socks4，socks5，最好使用 socks5

## 实现方式

通过 `proxychains` 实现，首先动态获取 windows 的真实 ip，然后修改 `proxychains` 的配置文件，使其连接 windows 中的代理应用。
尝试过 `export ALL_PROXY` 的方式实现，但兼容性不太理想，`iptables` 在新版 `wsl2` 中又有一些问题，所以目前只好这样实现。

### proxychains 已知问题

1. ICMP 无效，非 `socks5` 下 UDP 无效。
