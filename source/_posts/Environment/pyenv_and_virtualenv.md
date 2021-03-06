---
title: macOS中Python多版本管理与虚拟环境
date: 2019-03-10 22:25:37
summary: 通过pyenv版本管理和virtualenv虚拟环境进行python管理
img: https://gitee.com/wenguang0816/blogPic/raw/master/20190310-1.jpg
categories: 分享
tags:
  - macOS
  - Python
  - pyenv
  - virtualenv
---
## 多版本管理的优点
+ 当我们频繁开发和调试python程序时，会导致系统目录特别凌乱。
+ 不同开发用途可能会用到不同版本的python，不同的应用程序也可能需要不同版本的第三方库，这样在管理时会比较麻烦
因此我们引入**pyenv**版本管理和**virtualenv**虚拟环境。

## 安装pyenv版本管理
利用Homebrew进行安装
```bash
$ brew install pyenv
```

### 查看可安装的版本列表
```bash
$ pyenv install --list
```
我们可以看到有不同版本的python，例如python3.5.x和python3.6.x

### 安装python 3.5.2
这里以安装python 3.5.2为例
```bash
$ pyenv install 3.5.2
```
安装完毕后，我们可以查看安装情况
```bash
$ pyenv versions
```
显示结果如下
```
* system (set by /home/tony/.pyenv/version)
  3.5.2
```
system代表当前系统安装的python版本，3.5.2代表pyenv安装的python版本。

### 切换python版本
```bash
$ pyenv global 3.5.2
```
查看切换结果
```bash
  system
* 3.5.2 (set by /home/tony/.pyenv/version)
```
切换回系统默认版本
```bash
$ pyenv global system
```
卸载某一版本python
```bash
$ pyenv uninstall x.x.x
```

## 安装virtualenv虚拟环境
利用Homebrew安装
```bash
$ brew install pyenv-virtualenv
```

### 安装指定python版本的虚拟环境
```bash
$ pyenv virtualenv 3.5.2 env
```
该命令会创建名为`env`的虚拟环境，这个环境的真实目录位于：`~/.pyenv/versions/`
我们依然可以通过`pyenv versions`查看当前的虚拟环境安装情况
```bash
* system (set by /home/tony/.pyenv/version)
  3.5.2
  env
```
### 切换到虚拟环境
在切换到虚拟环境之前，我们还需要执行以下指令
```bash
$ eval  “ $（ pyenv init  - ） ”
$ eval  “ $（ pyenv virtualenv-init  - ） ”
```
通过一下命令切换到虚拟环境
```bash
$ pyenv activate env
```
我们可以通过`python`命令查看版本号
如果要退出虚拟环境，执行以下指令：
```bash
pyenv deactivate
```
如果需要删除虚拟环境，可以执行以下指令：
```bash
$ pyenv uninstall env
```
在实际应用过程中，多加利用这两个工具，可以让你的电脑整洁如新！
***
#### 补充
在最新系统Mojave 10.14中，执行`pyenv install 3.x.x`可能会出现以下错误：
```bash
$ zipimport.ZipImportError: can't decompress data; zlib not available
```
这个问题可能是macOS更新后，xcode没有跟进导致的，可以执行以下代码解决
```bash
$ sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
$ pyenv install 3.6.6
```
**参考博客：**[[Pluviophile's Blog
-Mojave使用pyenv安装python-zlib错误](https://lisupy.github.io/2018/10/01/2018-10-01-Mojave使用pyenv安装python/)