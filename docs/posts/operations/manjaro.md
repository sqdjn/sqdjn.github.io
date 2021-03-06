## 1.系统安装

### 1.1 启动u盘制作

- [rufus 下载](https://rufus.en.softonic.com/)（仅windows平台使用）注意使用后U盘恢复要使用 [DiskGenius](https://www.diskgenius.cn/)

- [Manjaro 镜像下载](https://manjaro.org.cn/category/download-manjaro) 使用KDE

### 1.2 硬盘分区

| 分区名       | 分区大小 | 格式 | 用处                 |
| ------------ | -------- | ---- | -------------------- |
| /boot        | 500MB    | ext4 | 引导区               |
| /boot/efi    | 500MB    | ext4 | 引导区               |
| swap交换空间 | 8GB      | swap | 充当内存，可以不设置 |
| /            | 50GB     | ext4 | 系统                 |
| /home        | 剩余所有 | ext4 | 用户空间             |



## 2. 基本设置

### 2.1 中文目录改成英文

将 `.config/user-dirs.dirs` 修改成如下：

```bash
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Download"
XDG_TEMPLATES_DIR="$HOME/Template"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_DOCUMENTS_DIR="$HOME/Document"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Picture"
XDG_VIDEOS_DIR="$HOME/"
```



### 2.2 网络设置

换源，从弹窗中选一个就行

```bash
sudo pacman-mirrors -i -c China -m rank
```

同步源并更新系统

```bash
sudo pacman -Syu
```

安装 yay

```bash
sudo pacman -S yay
```



## 3. 软件安装

### 3.1 科学上网

#### 1) Clash-1.8.0 (最新1.10.0)

**注意**：clash 版本可能影响代理的使用，和机场有关，所以不建议使用最新版本。

安装最新clash

```bash
yay -S clash
```

安装降级工具

```bash
yay -S downgrade
```

降级

```bash
sudo DOWNGRADE_FROM_ALA=1 downgrade clash
```

之后会让选择是否忽略更新，选y即可。或者手动编辑`/etc/pacman.conf`，添加

```bash
IgnorePkg = clash
```



##### 使用订阅

使用订阅地址转换网站，下载，移动到`~/.config/clash/config.yaml`



#### 2) proxychains

安装

```bash
yay -S proxychains
```

编辑 `/etc/proxychains.conf`，添加

```bash
socks5  127.0.0.1 port
http    127.0.0.1 port
```

yay 不能使用 proxychains，需要注释 `/etc/proxychains.conf`第52行的 proxy-dns



### 3.2 安装输入法

安装 fcitx5

```bash
yay -S fcitx-im
```

设置环境变量 `~/.pam_environment`

```bash
GTK_IM_MODULE DEFAULT=fcitx
QT_IM_MODULE  DEFAULT=fcitx
XMODIFIERS    DEFAULT=\@im=fcitx
SDL_IM_MODULE DEFAULT=fcitx
```

安装输入法

```bash
yay -S fcitx5-rime
yay -S rime-cloverpinyin
yay -S fcitx5-pinyin-zhwiki-rime#词库
yay -S fcitx5-material-color#主题
```

设置写入方案 `vim ~/.local/share/fcitx5/rime/default.custom.yaml`

```bash
patch:
  "menu/page_size": 5
  schema_list:
    - schema: clover
```



### 3.3 neovim 配置使用

[Neovim 配置实战：从0到1打造自己的IDE](https://juejin.cn/book/7051157342770954277)



### 3.4 其他软件

- timeshift 及时备份，小心翻车！

- typora markdown
- 查看硬件温度

```bash
yay -S i2c-tools
#查看cpu
watch -n 2 sensors
#查看gpu
watch -n 2 nvidia-smi
```

- s-tui

s-tui 可以查看cpu信息，而且可以烤鸡



## 4. 参考链接

感谢🙏🏻以下文章作者的分享

- [Manjaro-KDE安装配置全攻略](https://zhuanlan.zhihu.com/p/114296129)

- [Manjaro（Arch）软件包降级](https://blog.csdn.net/chen462488588/article/details/118786938)

- [在 linux 上使用 clash 订阅 ](https://hsingko.github.io/post/2021/07/05/how-to-use-clash-subscribe/)

- [解决proxychains不支持yay的问题](https://nopshore.top/posts/%E8%A7%A3%E5%86%B3proxychains%E4%B8%8D%E6%94%AF%E6%8C%81yay%E7%9A%84%E9%97%AE%E9%A2%98/)

