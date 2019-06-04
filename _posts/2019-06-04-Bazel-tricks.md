---
layout:     post   				    # 使用的布局（不需要改）
title:      Bazel stage 2 				# 标题 
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
