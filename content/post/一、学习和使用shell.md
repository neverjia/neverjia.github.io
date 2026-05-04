---
title: "shell基础"
slug: "shell基础"
date: "2025-05-14"
created: "2025-05-14"
tags: ["shell"]
---

### 一、为什么要学习和使用shell？

Shell属于内置的脚本，程序开发的效率非常高，依赖于功能强大的命令可以迅速地完成开发任务（批处理）语法简单，代码写起来比较轻松，简单易学（运维人员）

### Shell的分类

在linux中有很多类型的shell，不同的shell具备不同的功能，shell还决定了脚本中函数的语法，Linux中默认的shell是`/bash/shell`（ 重 点\默认 ），流行的还有`/bin/sh`、`/bin/bash`、`/usr/bin/sh`、`/usr/bin/bash`、`/bin/tcsh`、`/bin/csh`

**查看流行shell**

```
cat /etc/shells 
```

**当前系统使用的Shell**

```
echo $SHELL
```



## 二、Shell脚本入

### 文件命名规范

文件名`.sh` `.sh`是linux下bash shell 的默认后缀

### Shell解析器

指定告知系统当前这个脚本要使用的shell解释器

```
#!/bin/bash
```

### 第一个Shell程序“Hello World”

在根目录下创建一个"scripts"文件夹，用来存储文件

```
mkdir scripts
```

创建Shell文件

```
touch hello.sh
```

编辑Shell文件

```
#!/bin/bash
echo "Hello World"
```

执行脚本

```
bash ./hello.sh
sh ./hello.sh
```

更简单的执行方式，因为我们知道当前就在bash下面，所以可以直接执行文件

```
./hello.sh
```

此时你会发现，报错：`-bash: ./hello.sh: Permission denied`，这是因为没有权限，我们来查看权限

```
ll hello.sh # -rw-r--r--. 1 root root 31 Jun 21 05:41 hello.sh
```

接下来我们给他权限

```
chmod +x hello.sh
```

此时你会发现，文件变了颜色，所有可执行文件都会变颜色，变成绿色，执行文件

```
./hello.sh
```

扩展执行方案：

1. source 文件.sh
2. . 文件.sh


