---
layout:     post
title:      Introduction to Linux-shell
subtitle:   Introduction to Shell scripting
date:       2020-06-08
author:     Yingshan Li
header-img: img/sunrise.jpg
catalog: true
tags:
    - Linux
---

### Introduction

A shell script is a computer program designed to be run by the Unix shell, a command-line interpreter. The various dialects of shell scripts are considered to be scripting languages. Typical operations performed by shell scripts include file manipulation, program execution, and printing text.

### Creat shell scripts
创建一个test.sh文件

```
#!/bin/bash	告诉系统需要调用什么解释器
echo "Hello world!"
```

### Execute shell script

```
/bin/sh test.sh	直接运行bash命令执行shell脚本文件
```

```
chmod +x ./test.sh	先将脚本文件更改成可执行程序再执行
```

### Annotation
**单行注释：**每一行的行首加上#

**多行注释：**

```
:<<EOF

...

EOF
```

### I/O redirection

```
> file 以覆盖的方式将输出重定向到file
>>	file	以追加的方式将输出重定向到file
```

## Variable

#### Define a variable
shell可以直接定义变量，不需要想其它脚本语言如perl中那样在变量名前面加上特殊字符

```
name=“yingshanli”	注意变量名和等号之间不能有空格，所赋的值要用双引号括起来
```

除了直接定义变量外，还可以在语句中给变量赋值

```
for line in `cat reads.txt`
do
	echo "$line"
done
```

#### 使用变量
想上面那段代码一样，使用变量只需要在变量名前面加上美元符就可以了，我们建议将变量名用大括号括起来

#### 删除变量
unset命令可以删除变量

## String

**拼接字符串**

```
FirstName="yingshan"
LastName="Li"
FullName=${FirstName}${LastName}
```

**常用函数**

```
name="YingshanLi"
echo ${#name}		获取字符串长度，#表示number的意思
echo ${name:1:8}		提取子字符换
```

### Array

#### Create an array

```
Names=(YingshanLi Bob John)	用空格奖数组里的元素分开，同样数组名和等号之间不能有空格
```
或者

```
Names=(
YingshanLi
Bob
John
)	
```

#### 访问数组元素

```
echo ${Names[0]}		打印第一个名字
echo ${Names[@]}		打印所有名字
```

#### 获取数组大小

```
echo ${#Names[@]}
```

## Operators

### 算数运算符

```
a=8
b=6
expr $a+$b	返回“8+6”
expr $a + $b	返回14，注意expr后面的表达式每个元素都要用空格隔开
[ $a == $b ]	返回False，注意条件表达式里面每一个元素也要用空格分开
```

### 关系运算符

```
$a -eq $b	是否相等，注意横杠不能弄丢了
$a -ne $b
$a -gt $b
$a -lt $b
$a -ge $b
$a -le $b
```

### 逻辑运算符
**-a**: 表示and

**-o**: 表示or

```
if [ $a -gt 6 -a $b -lt 10]
then
echo "a is greater then 6 and b is smaller than 10"
else
echo "wrong"
fi
```

或者

**&&**: 表示and

**||**: 表示or

```
if [[ $a -gt 6 && $b -lt 10 ]]
then
echo "a is greater then 6 and b is smaller than 10"
else
echo "wrong"
fi
```

## Flow control

### if else

```
if [[ $a -gt 6 && $b -lt 10 ]]
then
echo "yes"
else
echo "wrong"
fi
```

写成一行

`if [[ $a -gt 6 && $b -lt 10 ]]; then echo "yes"; fi`

### Loop

**1. for loop**：

```
for line in `cat reads.txt`
do
	echo "$line"
done
```

One line

`for line in `cat reads.txt`; do echo "$line"; done`

**2. while loop**:

```
i=1
while(( $i<=10 ))
do
	echo "$line"
	let "$i++"
done
```

Infinite loop

```
while true
do
	echo "your computer is infected"
done
```

还有until和case循环，由于比较少用，在这里我就不过多介绍了，感兴趣的话可以找一些其它的资料看一看

**3. 跳出循环**：

**break**跳出整个大循环

**continue**跳出本次循环

## Parameter passing

很多时候我们需要利用命令行中的参数，可以用$n来获得。当执行命令`cat a.txt b.txt x.txt`后，$0的值为cat，$1的值为a.txt，$2的值为b.txt，以此类推

## Function

### Define a function

```
printname(){
	echo "My name is YingshanLi"
}

printname
```

### Function parameters

```
printname(){
	echo "The first name is $1"
	echo "The second name is $2"
	echo "The third name is $3"
}

printname YingshanLi Jim John
```
