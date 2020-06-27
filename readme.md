# wsl2proxy

让 wsl2 使用 windows 中的代理

## 安装

```shellscript
# 在 linux 子系统下执行
cd /usr/local && sudo git clone https://github.com/akirarika/wsl2proxy.git && cd wsl2proxy && sudo chmod +x ./wsl2proxy

# 接着在你使用的 shell 配置文件末尾添加
# 例：使用 `bash` 则在 `~/.bashrc`，`zsh` 在 `~/.zshrc`

```shellscript
# 向脚本传递两个参数，以指定你在 windows 下代理程序的协议和端口
# source /usr/local/wsl2proxy/wsl2proxy [协议] [端口]
source /usr/local/wsl2proxy/wsl2proxy socks5 7891

openProxy # 如果不希望每次开启终端时都自动打开代理，不加这行就好咯
```

配置好后重启终端即可。

## 使用

### 打开代理

```shellscript
openProxy
```

### 关闭代理

```shellscript
closeProxy
```

## 常见问题

### 端口号和协议配置的正确了，为什么还是连不上？

要在你的代理程序中允许局域网的请求，例在 `clash for windows` 中打开 `Allow LAN` 开关

### 协议类型可以填哪些？

http，https，socks4，socks5，最好使用 socks5

### 实现原理？

很简单的，看下源码你就秒懂了
