---
layout:     post   				    # 使用的布局（不需要改）
title:      Bazel stage 1 				# 标题 
#subtitle:   Hello World, Hello Blog #副标题
date:       2019-06-04 				# 时间
author:     Zihao 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - basel编译


### bazel build cpp example stage1
    编译vid2depth的时候，原程序提供的bazel编译icp_op， 当时觉得bazel麻烦，之前没有任何bazel的经验，就试图用camke来生成.so文件，
但是最终载入库的时候出了问题，可能是还要生成别的文件，但是用g++我只生成了一个icp_op.so文件。
    为了弄清问题在哪里，便从头学习bazel，首先看bazel编译cpp文件的历程，第一个例程是在stage1文件夹下，`bazel build //main:hello-world`
    
    然后报错
    `ERROR: /home/spadmin/research/examples/cpp-tutorial/stage1/main/BUILD:1:1: C++ compilation of rule '//main:hello-world' failed (Exit 1) gcc failed: error executing command /usr/lib/ccache/gcc -U_FORTIFY_SOURCE -fstack-protector -Wall -Wunused-but-set-parameter -Wno-free-nonheap-object -fno-omit-frame-pointer '-std=c++0x' -MD -MF ... (remaining 20 argument(s) skipped)

Use --sandbox_debug to see verbose messages from the sandbox
ccache: error: Failed to create file /home/spadmin/.ccache/tmp/tmp.cpp_stderr.anymal-beth-opc.2.Px9q3f: Read-only file system`
我没有注意到ccache error，而是吧注意力放在了error executing command这里，碰巧我把最后一条指令复制粘贴运行，没有任何反应，然后重新运行编译指令，竟然就可以了。
搞不懂为什么。 
    如果早点注意到ccache error 是无法创建文件的话，应该会先试试手动在该位置创建文件，然后再用sudo试试。

### 报错的指令
`/usr/lib/ccache/gcc -U_FORTIFY_SOURCE -fstack-protector -Wall -Wunused-but-set-parameter -Wno-free-nonheap-object -fno-omit-frame-pointer '-std=c++0x' -MD -MF bazel-out/k8-fastbuild/bin/main/_objs/hello-world/hello-world.pic.d '-frandom-seed=bazel-out/k8-fastbuild/bin/main/_objs/hello-world/hello-world.pic.o' -fPIC -iquote . -iquote bazel-out/k8-fastbuild/bin -iquote external/bazel_tools -iquote bazel-out/k8-fastbuild/bin/external/bazel_tools -fno-canonical-system-headers -Wno-builtin-macro-redefined '-D__DATE__="redacted"' '-D__TIMESTAMP__="redacted"' '-D__TIME__="redacted"' -c main/hello-world.cc -o bazel-out/k8-fastbuild/bin/main/_objs/hello-world/hello-world.pic.o`

### 显示依赖关系
https://blog.gmem.cc/bazel-study-note 这个里面给出的指令` 	
bazel query --nohost_deps --noimplicit_deps 'deps(//main:hello-world)' --output graph | xdot`不行，需要用`xdot <(bazel query --nohost_deps --noimplicit_deps 'deps(//main:hello-world)'  --output graph)`
  --output graph)
