# Homebrew 安装

## 基操

Homebrew 官方安装脚本是 Ruby 写的，Mac 自带 Ruby，所以直接执行 `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)` 即可。



## 问题

**但是！！！** 因为安装过程中的 `git` Homebrew 资源的速度极慢，导致安装过程还报错 ——

```c
error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
fatal: The remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
Failed during: git fetch origin master:refs/remotes/origin/master --tags --force
```



## 解决方法

**换源！！！** `(1～4)`

### 1、获取 Homebrew 安装脚本到本地

`curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install`

### 2、更改脚本中的资源链接

以清华源为例：

```ruby
BREW_REPO = "https://github.com/Homebrew/brew".freeze
```

替换为

```ruby
BREW_REPO = "https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git".freeze
```

### 3、执行安装脚本

`/usr/bin/ruby brew_install`

### 4、更换 Homebrew 更新源

```bash
# 替换 brew.git
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

# 替换 homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

# 替换 homebrew-bottles
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile

# 替换 cask 软件仓库（提供 macOS 应用和大型二进制文件，清华没有此源，用中科大的）
cd "$(brew --repo)/Library/Taps/caskroom/homebrew-cask"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

# 应用生效，这个会比较慢
brew update
```

### 5、重置源

有时候需要重置回官方源

``` bash
# 重置brew.git
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

# 重置homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git

# 重置 homebrew-bottles
# 直接修改之前创建的 .bash_profile 文件，或者直接删除 HOMEBREW_BOTTLE_DOMAIN 这个环境变量

# 应用生效
brew update
```

### 6、应用更新

在完成更新源的更换后，可以使用`brew upgrade`将现有的软件进行更新至最新版本，然后 `brew cleanup` 将旧有的软件安装包进行清理。



[原文](https://musoucrow.github.io/2017/03/29/brew_changing/)