# Python3 安装

Mac 目前是默认安装的 Python2

自带的 Python 的路径为 `/System/Library/Frameworks/Python.framework/Versions` ，其中 `Current` 目录下存放的是系统当前的 Python 版本



### 1、安装 brew

具体见 `brew.md`



### 2、`brew install python3`

有了 `brew` 一切都是这么简单，且安装的是最新稳定版本的，但并没有将 `python3` 命令链接到 `python` 

安装好之后，相关路径如下：

- 安装目录 —— `/usr/local/opt/python`

  具体的软件包（源码）目录 —— `/usr/local/opt/python/Frameworks/Python.framework/Versions/3.7`

  此外，在系统中的软件包（源码）目录 —— `/usr/local/Frameworks/Python.framework/Versions/3.7`

  此外，在 brew 中的软件包（源码）目录 —— `/usr/local/Cellar/python/3.7.3/Frameworks/Python.framework/Versions/3.7` （Homebrew 将软件包分装到单独的目录 `/usr/local/Cellar`，然后 symlink 到 `/usr/local` 中）

- `python` 命令目录 —— `/usr/local/bin/python3`

- 内置库目录 —— `/usr/local/Frameworks/Python.framework/Versions/3.7/lib/python3.7`

- pip 安装的第三方库目录 —— `/usr/local/lib/python3.7/site-packages`



### 3、更改 pip 源

在 `～` 目录下新建 `.pip` 目录，在 `.pip` 目录中新建 `pip.conf` 文件，即 pip 源的配置

**清华**

```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = pypi.tuna.tsinghua.edu.cn
```

**中科大**

```ini
[global]
index-url = http://pypi.mirrors.ustc.edu.cn/simple/
[install]
trusted-host = pypi.mirrors.ustc.edu.cn
```

**阿里**

```ini
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host = mirrors.aliyun.com
```

**豆瓣**

```ini
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host = pypi.douban.com
```

