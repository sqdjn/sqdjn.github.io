## 1. 基本命令

```bash
git config
--global #个人全局配置 ~/.gitconfig
--system #系统配置 /etc/gitconfig
--local #当前git目录配置 .git/config

unset 取消设置
```

#### 1.1 查看设置

```bash
git config --global --list
```

#### 1.2 设置用户名，邮箱

```bash
git config --global user.name "xxx"
git config --global user.email "xxxx@qq.com"
```

#### 1.3 设置代理

```bash
git config --global http.proxy http://127.0.0.1:port
git config --global https.proxy http://127.0.0.1:port
```

#### 1.4 取消代理

```bash
git config --global unset http.proxy
git config --global unset https.proxy
```

#### 1.5 修改创建默认为 main

```bash
git config --global init.defaultBranch main
```

#### 1.6 修改已创建项目的主分支为main

```bash
git branch -M main
```



## 2. ssh 设置

在～目录下，执行

```bash
#一路回车，在.ssh下生成 密钥和公钥
ssh-keygen -t rsa -C "zks458@qq.com"
cd .ssh
cat id_rsa.pub
```

把公钥复制到 Github 网站中就行了
