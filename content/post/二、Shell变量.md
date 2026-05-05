---
title: "shell变量"
slug: "shell变量"
date: "2025-12-1"
created: "2025-12-1"
tags: ["shell"]
---

## 一、Shell变量_系统预定义变量

### 1、运行Shell文件的区别

第一种：`bash ./hello.sh` 和 `sh ./hello.sh`

第二种：`source hello.sh` 和 `. hello.sh`

两种运行的方式差异性在于，第一种是在子bash环境下运行，而第二种是在当前bash环境下运行，我们通过运行`type source`可以看到 `source is a shell builtin` （source 是 shell 内嵌）

我们执行`ps -f`可以查看当前bash环境，创建一个子bash，继续通过`ps -f`查看，在当前子bash环境下，你依然可以运行shell文件

从结果上来看，两者好像没有什么区别，但是如果引入更多知识，例如变量：**如果子shell中设置的当前变量，父shell是可不见的**

### 2、变量简介

变量本质上其实是在内存中开辟一个空间用来临时存储数据，例如：`age = 20

- 全局变量
- 局部变量
- 系统预定义变量
- 用户自定义变量

#### 全局变量和局部变量的区别

`全局变量：层层嵌套的子bash依然可以访问`

`局部变量：只在当前的bash中可以访问，子bash和父bash都不能访问呢`

#### 常用系统变量

```
$HOME 、$PWD 、$SHELL 、$USER

查看当前所有的全局系统变量`env`
查看当前所有的变量`set`(包含全局和局部的，系统的，用户的)
```

## 二、Shell变量_用户自定义变量

### 基本语法

`定义变量：变量名=变量值`

规则

1. 等号前后不能有空格
2. 在声明变量的时候是不需要添加`$`符号,但是使用时候需要添加
3. 如果定义的是一个字符串，需要将值添加双引号或者单引号

> **温馨提示**
>
> 查看定义的变量是全局还是局部
>
> 全局：`env | grep 变量名`
>
> 局部：`set | grep 变量名`
>
> 当然，你可以进入子bash中去尝试输出变量，无法输出则是局部变量，可以输出则是全局变量

### 全局变量

如何定义一个全局变量呢？需要先声明一个局部变量，然后再通过`export`导出为一个全局变量

```
export 变量名
```

> **温馨提示**
>
> 再子bash中修改全局变量，只会再当前环境中生效，不会影响父bash环境，哪怕是你增加`export`也依然不会影响到父bash环境

### Shell脚本中使用变量

我们可以在`hello.sh`的脚本中去调用全局和局部变量

```
#!/bin/bash
echo $txt
```

> **温馨提示**
>
> 在shell脚本中使用变量，同样遵循全局和局部变量的规则



## 三、Shell变量_只读变量和撤销变量

### 自定义变量注意事项：

1. 变量命名规范：字母、数字和下划线组成，其中数字不能开头
2. 自定义变量一般都是小写的
3. 在shell中，变量是没有类型的，或者我们理解为全部都是字符串类型
4. 如果变量的值需要做数值运算，可以使用`$((1+1))`或者`$[1+1]`的形式

### 只读变量

在shell中，只读变量相当于是常量，定义之后不允许修改。定义规则

```
readonly 变量名=值
```

### 撤销变量

变量定义之后是可以撤销的，使用`unset 变量名`就可以撤销了

> **温馨提示**
>
> 变量是可以撤销的，但是只读变量是不可以撤销的

## 四、Shell变量_特殊变量

在Shell中，存在一些特殊变量，他们具有特殊的意义

### $n

`$n`代表接受参数，`n`是数字，代表在执行脚本时候传递的参数数量，例如`$1-$9`代表第一个到第九个参数，十以上的数字，可以使用大括号包裹，例如`${10}`。比较特殊的是`$0`,代表当前脚本名称

```
#!/bin/bash
echo '======$n====='
echo 1st:$1
echo 2st:$2
echo 3st:$3
echo $0
```

### $#

`$#`获取输入参数的个数，一般用于循环中，判断参数的个数是否正确，加强脚本的健壮性

```
#!/bin/bash
echo '=====$#====='
echo 1st:$1
echo 2st:$2
echo 3st:$3
echo $#
```

### `$*`和`$@`

`$*`和`$@`非常相似，都代表命令行所有的参数，但是`$*`把参数看成是一个整体，例如`123 456`。而`$@`把每个参数区分对待，例如`[123,456]` **注意：在没有循环遍历时候，两者效果一致**

```
#!/bin/bash
echo '=====$n====='
echo 1st:$1
echo 2st:$2
echo 3st:$3
echo '=====$*====='
echo $*
echo '=====$@====='
echo $@
```

### $?

`$?`最后一次执行命令的状态，如果是结果是0，证明上面执行的命令都是正确的，如果结果不是0(具体是哪个数字，有命令自己决定)，则证明上面命令不正确了

```
[root@localhost scripts]# vim hello.sh
[root@localhost scripts]# echo $?
0
[root@localhost scripts]# hello.sh
-bash: hello.sh: command not found
[root@localhost scripts]# echo $?
127
[root@localhost scripts]# 
```



## Shell_条件判断(一)

Shell中也有条件表达式，也就是比较两个值是否相等

### 基本语法

```
test 表达式
[ 表达式 ]  注意：中括号前后需要有空格
[root@localhost scripts]# a=10
[root@localhost scripts]# echo $a
10
[root@localhost scripts]# test $a = 10
[root@localhost scripts]# echo $?
0
[root@localhost scripts]# test $a = 11
[root@localhost scripts]# echo $?
1
[root@localhost scripts]# [ $a = 10 ]
[root@localhost scripts]# echo $?
0
[root@localhost scripts]# [ $a = 11 ]
[root@localhost scripts]# echo $?
1
[root@localhost scripts]# [ $a=11 ]
[root@localhost scripts]# echo $?
0
[root@localhost scripts]# [  ]
[root@localhost scripts]# echo $?
1
[root@localhost scripts]# [ $a != 11 ]
[root@localhost scripts]# echo $?
0
[root@localhost scripts]# echo $a
10
```

## Shell_条件判断(二)

在条件判断中，除了相等于不等的判断，还有一些其他的判断

### 两个值比较

| 表达式 | 含义               | 表达式 | 含义                      |
| ------ | ------------------ | ------ | ------------------------- |
| -eq    | 等于(equal)        | -ne    | 不等于(not equal)         |
| -lt    | 小于(less than)    | -le    | 小于等于(less equal)      |
| -gt    | 大于(greater than) | -ge    | 大于等于（greater equal） |

### 文件权限判断

1. `-r` 有读的权限(read)
2. `-w` 有写的权限(write)
3. `-x` 有执行的权限(execute)

### 文件类型判断

1. `-e` 文件存在(existence)
2. `-f` 文件存在并且是一个文件类型(file)
3. `-d` 文件存在并且是一个目录类型(directory)

### 多条件判断

`&&` 与的关系，两者都成立

`||` 或的关系，两者有一个成立

> **温馨提示**
>
> `&&` 表示前一个条命令执行成功之后，在执行第二个条件
>
> `||` 表示前一个条命令执行失败之后，再执行第二个条件
>
> 由此，我们可以衍生出来，类似三元运算符的形式
>
> 示例 `[ $a -eq $b ] && echo "$a=$b" || echo "$a!=$b"`