---
title: Queue、Deque小结
categories: 个人学习
tags:
  - 学习
  - Java
keywords: Queue、Deque、LinkedList、ArrayDeque
description: 总结了一下Queue、Deque的特点和方法，避免记混
abbrlink: cfc17fc4
date: 2024-01-03 16:06:14
---

<font face="楷体" size=24><span style="background:#eef0f4;color:Chocolate">Queue的原理：</span></font>

​        Queue，队列，以`先进先出`的方式访问和存储元素，也就是说，**从后面添加元素，从前面删除元素**。

​		它的实现有以下三种方式：

![ArrayDeque，LinkedList和PriorityQueue在Java中实现了Queue接口。](https://real-jack.oss-cn-beijing.aliyuncs.com/undefinedqueue-interface.png)

```java
// 使用 LinkedList 创建
Queue<String> animal1 = new LinkedList<>();

// 使用 ArrayDeque 创建
Queue<String> animal2 = new ArrayDeque<>();

// 使用 PriorityQueue创建 （优先级队列）
Queue<String> animal3 = new PriorityQueue<>();
```



<font color="red">Queue的方法与Deque类似，就是只有队列头部删除、尾部增加的方法，所以就以Deque为例进行总结。</font>



<font face="楷体" size=24><span style="background:#eef0f4;color:Chocolate">Deque的常用方法：</span></font>

### <font face="楷体"><span style="background:#eef0f4;color:DarkCyan">Deque的常用方法——添加元素</span></font>

* **add()** - 将指定的元素插入队列尾部。如果任务成功，则add()返回true，否则将引发异常。
* **addFirst()** - 将指定的元素插入队列头部。如果任务成功，则addFirst()返回true，否则将引发异常。
- **offer()** - 将指定的元素插入队列尾部。如果任务成功，则offer()返回true，否则返回false。
- **offerFirst()** - 将指定的元素插入队列头部。如果任务成功，则offerFirst()返回true，否则返回false。
- **push()** - 将指定的元素插入队列头部。如果任务成功，则push()返回true，否则返回false。



### <font face="楷体"><span style="background:#eef0f4;color:DarkCyan">Deque的常用方法——查看元素</span></font>

- **element()** - 返回队列的开头。如果队列为空，则引发异常。
- **peek()** - 返回队列的开头。 如果队列为空，则返回null。
- **getFirst()** - 返回队列的开头。 如果队列为空，则返回null。
- **getLast()** - 返回队列的结尾。 如果队列为空，则返回null。



### <font face="楷体"><span style="background:#eef0f4;color:DarkCyan">Deque的常用方法——删除元素</span></font>

- **remove()** - 返回并删除队列的头部。如果队列为空，则引发异常。
- **removeLast()** - 返回并删除队列的尾部。如果队列为空，则引发异常。
- **poll()** - 返回并删除队列的开头。 如果队列为空，则返回null。
- **pollLast()** - 返回并删除队列的尾部。 如果队列为空，则返回null。
- **pop()** - 返回并删除队列的开头。 如果队列为空，则引发异常。



### <font face="楷体"><span style="background:#eef0f4;color:DarkCyan">Deque的其余方法</span></font>

* **contains()** - 检查队列是否包含该元素。如果队列不包含，则返回false，包含返回true。
* **size()** - 返回队列中存储元素的个数。
* **isEmpty()** - 返回队列中元素是否为空。
* **for-each循环** - 迭代队列中的元素。
* **iterator（）** - 迭代队列中的元素。

```java
//通过迭代器迭代Deque 
Deque<String> deque = new LinkedList<>();
 
deque.add("element 0");
deque.add("element 1");
deque.add("element 2");
 
Iterator<String> iterator = deque.iterator();
while(iterator.hasNext(){
  String element = iterator.next();
}
```



<font face="楷体" size=24><span style="background:#eef0f4;color:Chocolate">Queue的常用方法：</span></font>

|                    | throw Exception | 返回false或null    |
| :----------------- | :-------------- | :----------------- |
| 添加元素到队尾     | add(E e)        | boolean offer(E e) |
| 取队首元素并删除   | E remove()      | E poll()           |
| 取队首元素但不删除 | E element()     | E peek()           |
