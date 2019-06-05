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

### 用copts给编译器添加参数
比如在非标准的包含路上上，
```
cc_library(
    name = "some_lib",
    srcs = ["some_lib.cc"],
    hdrs = ["include/some_lib.h"],
    copts = ["-Ilegacy/some_lib/include"],
)

```
### 无sudo权限安装bazel
参照[bazel教程](https://docs.bazel.build/versions/master/install-ubuntu.html "悬停显示")来局部安装bazel，谢谢Andrei的提醒，不然还在困惑怎么在没有sudo权限的时候安装bazel。

具体参见其中的Installing using binary installer条目
