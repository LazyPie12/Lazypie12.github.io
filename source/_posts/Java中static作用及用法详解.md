---
title: Java中static作用及用法详解
date: 2020-07-26 03:20:02
toc: true
categories: Java基础
tags: 
---

### 1. 概述

在程序中任何变量或者代码都是在编译时由系统自动分配内存来存储的，而所谓静态就是指在编译后所分配的内存会一直存在，直到程序退出内存才会释放这个空间，也就是只要程序在运行，那么这块内存就会一直存在。在Java程序里面，所有的东西都是对象，而对象的抽象就是类，对于一个类而言，如果要使用他的成员，那么普通情况下必须先实例化对象后，通过对象的引用才能够访问这些成员，但是用static修饰的成员可以通过**类名加 “.” **进行直接访问。

<!--more-->

被static修饰的成员变量和成员方法独立于该类的任何对象。也就是说，它不依赖类特定的实例，被类的所有实例共享。只要这个类被加载，Java虚拟机就能根据类名在运行时数据区的方法区内定找到他们。因此，static对象可以在它的任何对象创建之前访问，无需引用任何对象。

</br>

### 2. 定义和使用格式

#### 类变量

当 ```static``` 修饰成员变量时，该变量称为**类变量**（没被修饰的变量称为**实例变量**）。该类的每个对象都**共享**同一个类变量的值。任何对象都可以更改该类变量的值，但也可以在不创建该类的对象的情况下对类变量进行操作。  

定义格式：

``` java
static 数据类型 变量名;
```

举例：

``` java
static String name;
```

比如说，基础班新班开班，学员报到。现在想为每一位新来报到的同学编学号（id），从第一名同学开始，id为1，以此类推。学号必须是唯一的，连续的，并且与班级的人数相符，这样以便知道，要分配给下一名新同学的学号是多少。这样我们就需要一个变量，与单独的每一个学生对象无关，而是与整个班级同学数量有关。

所以，我们可以这样定义一个静态变量numberOfStudent，代码如下：  

```java
public class Student {
	private String name;
	private int age;
	// 学生的id
	private int id;
	// 类变量，记录学生数量，分配学号，初始化为0
	public static int numberOfStudent = 0;
    
	public Student(String name, int age){
    	this.name = name;
		this.age = age;
		// 通过 numberOfStudent 给学生分配学号
		this.id = ++numberOfStudent;
	} 
   	
    // 打印属性值
	public void show(){
		System.out.println("Student : name=" + name + ", age=" + age + ", sid=" + id);
	}
}

public class StuDemo {
	public static void main(String[] args) {
        Student s1 = new Student("张三", 23);
        Student s2 = new Student("李四", 24);
        Student s3 = new Student("王五", 25);
        Student s4 = new Student("赵六", 26);
        s1.show(); // Student : name=张三, age=23, sid=1
        s2.show(); // Student : name=李四, age=24, sid=2
        s3.show(); // Student : name=王五, age=25, sid=3
        s4.show(); // Student : name=赵六, age=26, sid=4
	}
}
```

#### 静态方法

当 ```static``` 修饰成员方法时，该方法称为**类方法** 。静态方法在声明中有 ```static``` ，**建议直接使用类名来调用**，而不需要创建类的对象。调用方式非常简单。  

定义格式：

```java
修饰符 static 返回值类型 方法名 (参数列表){
	// 执行语句
}
```

举例：在Student类中定义静态方法 

```java
public static void showNum() {
	System.out.println("num:" + numberOfStudent);
}
```

- 静态方法调用的注意事项：
  - 静态方法可以直接访问类变量和静态方法。
  - 静态方法不能直接访问普通成员变量或成员方法。但是，成员方法可以直接访问类变量或静态方法。
  - 静态方法中，不能使用this或super关键字。

> 小贴士：静态方法只能访问静态成员  

#### 调用格式

被static修饰的成员可以并且建议通过**类名直接访问**。虽然也可以通过对象名访问静态成员，原因即多个对象均属于一个类，共享使用同一个静态成员，但是不建议，会出现警告信息。  

格式：

```java
// 访问类变量
类名.类变量名；
    
// 调用静态方法
类名.静态方法名(参数)；
```

调用演示：

```java
public class StuDemo2 {
    public static void main(String[] args) {
    // 访问类变量
    System.out.println(Student.numberOfStudent);
    // 调用静态方法
    Student.showNum();
	}
}
```

</br>

### 3. 静态代码块

static代码块也叫静态代码块，是在类中独立于类成员的static语句块，可以有多个，位置可以随便放，它不在任何的方法体内，JVM加载类时会执行这些静态的代码块，如果static代码块有多个，JVM将按照它们在类中出现的先后顺序依次执行它们，每个代码块只会被执行一次。

格式：

```java
public class test {
	static {
		//执行语句
    }
}
```

作用：给类变量进行初始化赋值。用法演示，代码如下：  

```java
public class Game {
    public static int number;
    public static ArrayList<String> list;
    
    static {
    	// 给类变量赋值
        number = 2;
        list = new ArrayList<String>();
        // 添加元素到集合中
        list.add("张三");
        list.add("李四");
    }
}
```

</br>

### 4. 总结

有时你希望定义一个类成员，使它的使用完全独立于该类的任何对象。通常情况下，类成员必须通过它的类的对象访问，但是可以创建这样一个成员，它能够被它自己使用，而不必引用特定的实例。在成员的声明前面加上关键字static就能创建这样的成员。如果一个成员被声明为static，它就能够在它的类的任何对象创建之前被访问，而不必引用任何对象。你可以将方法和变量都声明为static。static 成员的最常见的例子是main( ) 。因为在程序开始执行时必须调用main() ，所以它被声明为static。

static 关键字，可以修饰变量、方法和代码块。在使用的过程中，其主要目的还是想在不创建对象的情况下，去调用方法。

