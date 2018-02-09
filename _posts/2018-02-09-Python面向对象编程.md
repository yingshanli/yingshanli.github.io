---
layout:     post
title:      Python面向对象编程
subtitle:   介绍Python的面向对象编程，包括封装、继承和多态等重要概念
date:       2018-02-09
author:     Yingshan Li
header-img: img/bamboo.jpg
catalog: true
tags:
    - Python
---


## 面向对象

按照我的理解，面向对象就是把很多细节封装起来，在计算机编程语言当中，这些细节就包括数据，数据结构和方法函数，这极大地降低了代码的编写和阅读难度，极大地避免了重新造轮子。比如如果我想生产一台电脑，如果按照传统的面向过程的思路，那我们就要从头来思考该怎么样来构建一台电脑，从每一根电线，每一个开关开始造，这是非常非常复杂的，而如果用面向对象的思路，我们只需要把一台电脑的几个重要组成部分就可以组装出一台电脑，比如CPU，硬盘，主板，GPU，网卡等等，而CPU内部的细节都被封装起来了，只需要给一个接口我就可以直接调用里面的所有功能，这样在生产电脑的时候就不需要反复的重新造轮子了。在Python里面，一切皆为对象，例如一个list，一个dictionary，一个函数，一个类等等。当你创建了一个list对象之后，你就可以调用这个对象的方法了，比如length()方法。

## 类和实例

抽象的能力可能是人类最引以为豪的能力之一了，在日常生活和科学研究中抽象处处可见，例如我们说"人""苹果"这样的概念就是抽象的，而具体的一个人和一个苹果就是这个抽象的一个实例，不同的人和不同的苹果之间又有一些差异，但是我们仍然能够分辨出来这是一个人还是一个苹果，这是因为不同的苹果之间虽然有差异，但是他们又有很多的本质上的相同点，比如他们都有语言能力等等。这就是我们面向对象编程中类和实例的基本思想。

定义一个类：

```
class ClassName:
	statement
```
举个例子：

```
class human:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
	def hello(self):
		print("Hello, I'm", self.name)
		
person1 = human("Yingshan", 25)
person2 = human(age=23, name="Lee")
```
这样就创建了一个人(human)的实例，也就是一个person。

## 属性和方法

上面那个例子引出了另外两个概念，属性和方法。一个类对象就是具有相同属性和方法的实例的0集合，比如一个人的名字和年龄等等就是人的属性，能够说“hello”就是人特有的方法，当然还可以有其它的属性和方法。

创建类的时候我们通过```__init__```的特殊函数来绑定这个类的属性，注意前后都有两个下划线。```__init__```函数第一个参数是self，表示实例本身，然后就是其它的参数，和别的函数没有什么不同。

定义类的方法和定义一个普通函数基本相同，但是第一个参数一定是self，这样在创建一个实例的时候，这个实例自然拥有了这个方法(函数)，比如能够说hello。

调用类的属性和方法很简单，只需要用点号引用就好了，object.name

## 继承和多态

继承和多态应该是最能体现面向对象编程核心思想的了，继承的意思应该比较好理解，前面我们提到了类的概念，就是拥有同样属性和方法的全部实例的集合，比如所有有语言能力的个体抽象成"人"。那么比人更加抽象的概念有哪些呢？很简单，你可以说人是"动物"，也可以接着说人是"真核生物"，还可以接着说人是"生物"。因此，凡是"动物"这个类所拥有的属性，人应该全部拥有，不需要重新定义，只需要直接继承下来就可以了。但是反过来就不行了，因为不是所有的动物都是人类，不是所有的真核生物都是动物。

```
class animal():
	def mobile(self):
		return ("Yes, animal are mobile")

class human(animal):
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
	def hello(self):
		print("Hello, I'm", self.name)
```
这样，human这个类就直接继承了animal这个类中的方法，所有的human实例都可以直接调用animal的方法。我们称human为子类，animal为父类。

有的人可能已经想到了，如果父类和子类拥有相同的方法，但是我又不想完全继承父类的方法怎么办？比如，动物能动，人也能动，但是我不希望人运动的方式和其它的动物完全一样。这种情况下，你只需要在子类里面重新定义一下mobile这个方法就好了，因为子类的方法会自动覆盖父类的方法。

```
class animal():
	def mobile(self):
		return ("Yes, this animal is mobile")

class human(animal):
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
	def hello(self):
		print("Hello, I'm", self.name)
		
	def mobile(self):
		return ("Yes, this person is mobile")
```



