---
title: CentOS6.x 手动升级gcc版本
date: 2016-08-17 10:08:25
tags: [CentOS, gcc, c++]
---
关于CentOS 6.x gcc 默认版本
<!-- more -->
由于CentOS6.x的版本默认的gcc版本是4.4.7，不支持c++11的特性，所以我在拿到之后升级了一下gcc，但是当时在选择版本的时候看到了6.1.0想了一下最新版可能有坑就选择了5.4.0.。。事实证明，应该和系统选择一致的版本。。。于是在尝试编译出现了和4.8.x不太一样的东西的时候。。。无奈又要重新再安装一下4.8.4 所以准备记录一下过程


首先是获取gcc的压缩包，你可以去
[http://ftp.gnu.org/gnu.gcc](http://ftp.gnu.org/gnu.gcc)里面去挑选你想要的版本
我选择的是4.8.4
```bash
$ wget http://ftp.gnu.org/gnu/gcc/gcc-4.8.4/gcc-4.8.4.tar.bz2
$ tar -jxvf gcc-4.8.4.tar.bz2
```
解压之后回省城一个目录
```bash
$ cd gcc-4.8.4
$ ./contrib/download_prerequisites
```
这里gcc-4.8.4/contrib/download_prerequisites 这个脚本可以帮我们把依赖的环境都下载好安装好，无需再麻烦。。。非常方便
之后建议建立一个目录用来编译gcc，会产生很多编译出来的文件
```bash
$ cd ..
$ mkdir gcc-build-4.8.4
$ cd gcc-build-4.8.4
```
生成makefile
```bash
$ ../gcc-4.8.4/configure -enable-checking=release -enable-languages=c,c++ -disable-multilib
```
之后就编译吧
```bash
$ make -j4
```
这里-j4是一个优化开关，如果不支持就直接make也可以，这一步会很长时间
结束之后
```bash
$ sudo make install
$ gcc -v
```
安装一下，查看版本
另外提一句。gcc -v查看到可能会发现还是之前的版本，尝试重启或者断开ssh重连一下应该就好，如果还没好说明安装哪一步出了问题，正常情况下应该就可以用了。


