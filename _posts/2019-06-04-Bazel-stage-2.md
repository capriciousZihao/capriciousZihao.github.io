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

### bazel build cpp example stage2
运行stage2的例程的时候，还是出现了和stage1相同的问题，照着stage1的小聪明，重新运行错误部分的指令，但是这次并没有解决问题

用“bazel ccache error failed to create file”搜索，发现问题是由于sanbox和ccache冲突，解决办法就是要么不用ccache，要么不用sandbox，
不用sandbox的话，加入两个参数，最终指令如`bazel build --strategy=CppCompile=standalone --strategy=CppLink=standalone src:bazel`
