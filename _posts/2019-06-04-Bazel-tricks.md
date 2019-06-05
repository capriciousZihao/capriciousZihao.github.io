---
layout:     post   				    # 使用的布局（不需要改）
title:      Bazel tricks 				# 标题 
#subtitle:   Hello World, Hello Blog #副标题
date:       2019-06-04 				# 时间
author:     Zihao 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - basel编译
---

## 用copts给编译器添加参数
比如在非标准的包含路上上，
```
cc_library(
    name = "some_lib",
    srcs = ["some_lib.cc"],
    hdrs = ["include/some_lib.h"],
    copts = ["-Ilegacy/some_lib/include"],
)

```
## 无sudo权限安装bazel
参照[bazel教程](https://docs.bazel.build/versions/master/install-ubuntu.html "悬停显示")来局部安装bazel，谢谢Andrei的提醒，不然还在困惑怎么在没有sudo权限的时候安装bazel。

具体参见其中的Installing using binary installer条目

## build vid2depth
### 尝试各种版本的bazel
尝试了0.7，0.26, 0.23,参考某网友的意见，最后选择0.17.2

### no such package '@hdf5//
- 原因 原来的文件中使用的链接无效了
- 解决方法 
  * 1- 根据错误提示，找出链接对应的文件, for example, `grep -lir "https://support.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.10.1.tar.gz" /home/zihaox/
 `
  * 2- 打开文件，将对应的链接替换成可以正常下载的链接
  `#url = "http://www.bzip.org/1.0.6/bzip2-1.0.6.tar.gz",
   url = "https://fossies.org/linux/misc/bzip2-1.0.6.tar.gz"`

### 改动文件列表 
- 和bzib2有关的文件boost.bzl 
- 和hdf5 有关的文件WORKSPACE
