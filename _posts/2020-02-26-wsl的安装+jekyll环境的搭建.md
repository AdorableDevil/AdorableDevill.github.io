---
title: wsl的安装+jekyll在wsl环境下的搭建
tags: 博客搭建
layout: post
---
## What is WSL
> wsl 简单地说是windows下的Linux子系统。    
Windows Subsystem for Linux（简称WSL）是一个在Windows 10上能够运行原生Linux二进制可执行文件（ELF格式）的兼容层。它是由微软与Canonical公司合作开发，其目标是使纯正的Ubuntu 14.04 "Trusty Tahr"映像能下载和解压到用户的本地计算机，并且映像内的工具和实用工具能在此子系统上原生运行。

## LxRunOffline

> 说到WSL，不得不提一个非常好用WSL管理软件：LxRunOffline。它可以安装任意发行版到任意目录、转移已安装的 WSL 目录、备份 WSL、设置默认用户和修改环境变量等操作，完全碾压 wsl、wslconfig 这些简陋原生管理命令。

## 准备

 1.打开windows开发者模式
![如图例](https://gitee.com/adameta/img/raw/master/1578725783_20200111144223121_9117.png)

2.打开windows子系统服务
控制面板->程序和功能->启用或关闭Windows功能->勾选 适用于Linux的Windows子系统

![如图示](https://images2017.cnblogs.com/blog/723701/201801/723701-20180103223038768-1629438015.png)

3.win+x+a打开powershell。键入
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

##### （输完命令后需要重启电脑）

## 下载 wsl 离线安装包
- [wsl安装包下载](https://docs.microsoft.com/en-us/windows/wsl/install-manual)

## 下载LxRunOffline
- [LxRunOffline安装包下载](https://github.com/DDoSolitary/LxRunOffline/releases)

## 安装
1.将下载的wsl文件从appx改名为zip后缀。例如：
![](https://gitee.com/adameta/img/raw/master/1578725783_20200111144918195_20181.png)

2.解压wsl的zip文件与LxRunOffline。

3.将LxRunOffline的路径加入环境变量
![](https://lukebest.github.io/posts/bb32/20190326151814.png)

4.若测试如下，则说明LxRunOffline安装正常。
![](https://gitee.com/adameta/img/raw/master/1578725784_20200111145202578_10904.png)

5.win+x+a打开powershell。键入
> LxRunOffline i -n <安装名称> -d <安装路径> -f <安装文件>

其中安装名称可以自定义，安装路径为自定义安装路径，安装文件为上一步解压后的文件中的 install.tar.gz 的路径，回车后等待安装完成。示例如下：
![](https://gitee.com/adameta/img/raw/master/1578725781_20200111143121057_26638.png)
随后桌面出现图标，现在即为被管理起来的wsl。

![](https://gitee.com/adameta/img/raw/master/1578725784_20200111145609029_5369.png)

之后点开上述图标便可以愉快的使用wsl了。

#### ps:我装的时候遇到了一个问题，安装完点开是黑屏，无响应。

![](https://img-blog.csdnimg.cn/20200226181049713.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)
亦或是：
![](https://img-blog.csdnimg.cn/20200226181254849.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)

##### ps:只要重启一下应该就可以解决

正常显示如下：
![](https://img-blog.csdnimg.cn/20200226181715174.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)

## jekyll在wsl环境的搭建

#### 在搭建前首先介绍一下What is jekyll

> - [jekyll简介](https://jekyllcn.com/)


##### 接下来搭建jekyll

1.打开刚刚的命令行
![](https://img-blog.csdnimg.cn/20200226181715174.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)

2.更新一下环境
> sudo apt update -y
sudo apt upgrade -y

##### 如果此更新环境过程缓慢，建议把你apt源从ubuntu官方改到阿里云镜像,输入以下指令：

>sudo sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list

然后再执行上述两条指令。

3.输入以下指令：
>sudo apt install -y ruby ruby-dev zlib1g.dev make gcc g++
sudo gem install bundler

##### 如果输入完命令行无响应或者反应缓慢,如下图所示:

![](https://img-blog.csdnimg.cn/20200226182654418.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)
##### 按顺序执行以下几条命令
> sudo apt install -y ruby ruby-dev zlib1g.dev make gcc g++
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
sudo gem install bundler
bundle config mirror.https://rubygems.org https://gems.ruby-china.com

4.依次执行下述指令，可以自动下载并部署博客的所有依赖。
> 
(1) git clone+你的仓库的链接
>
eg: git clone https://github.com/AdorableDevil/AdorableDevil.github.io.git
>
(2) 进入你仓库的目录
>
(3) cd +你把文件下载的路径
>
(4) bundle install
>
(5) bundle exec jekyll s
>
若你看到
> 
Server address: http://127.0.0.1:4000/
>
Server running... press ctrl-c to stop.

说明你安装成功了，图例：
![](https://img-blog.csdnimg.cn/20200226184007769.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)
点击 http://127.0.0.1:4000/ 尽情预览你的网页吧！
##### ps:如果你遇到这种情况：
![](https://img-blog.csdnimg.cn/20200226184356669.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20200226184325270.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)
##### 把wsl关掉重开一遍就好了。
得到预览如图所示：
![](https://img-blog.csdnimg.cn/20200226184852198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Fkb3JhYmxlRGV2aWw=,size_16,color_FFFFFF,t_70)

最后再次感谢提供资料与很多帮助的[wu-kan](https://wu-kan.cn/)与[oceanlvr](https://adameta.top/)。

参考链接：

1.https://www.cnblogs.com/adameta/p/12179922.html

2.https://wu-kan.cn/_posts/2019-01-18-%E5%9F%BA%E4%BA%8EJekyll%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/

###### 有什么问题可以在下方给我留言哦~<br/>