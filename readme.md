# wsl2proxy

让 wsl2 使用 windows 中的代理

## 安装

```shellscript
# 在 linux 子系统下执行
cd /usr/local && sudo git clone https://github.com/akirarika/wsl2proxy.git && cd wsl2proxy && sudo chmod +x ./wsl2proxy

# 接着在你使用的 shell 配置文件末尾添加
# 例：使用 `bash` 则在 `~/.bashrc`，`zsh` 在 `~/.zshrc`

```shellscript
source /usr/local/wsl2proxy/wsl2proxy
openProxy # 如果不希望每次开启终端时自动打开代理，则不输入此行
```

配置好后重启终端即可

## 使用

### 打开代理

```shellscript
openProxy
```

### 关闭代理

```shellscript
closeProxy
```