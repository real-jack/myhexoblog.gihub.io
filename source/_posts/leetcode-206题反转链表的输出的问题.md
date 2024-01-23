---
title: leetcode-206题反转链表的输出的问题
categories: Github
tags:
  - Java
  - 学习
description: 发现了一个leetcode输出的问题。
abbrlink: 3f4948d6
date: 2023-12-29 10:50:47
keywords:
---

最近在leetcode做206这个反转链表的时候，发现最终输出newH.next的时候有点问题，特此记录一下。
<!-- more-->

先看题目：

**206.反转链表**

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

**示例1：**

![img](https://real-jack.oss-cn-beijing.aliyuncs.com/undefinedrev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例2：**

![img](https://real-jack.oss-cn-beijing.aliyuncs.com/undefinedrev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```



#### <span style="background:#eef0f4;color:blue">我的正常答案：（双指针法）</span>

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null, cur = head;
        ListNode tmp;
        while(cur != null){
            tmp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
}
```



### <span style="background:#eef0f4;color:red">但是，有意思的事情发生了，当我尝试的返回`pre.next`，它却返回的是null？</span>

按我的个人理解，这当然是一个错误答案，但正确的返回应该是排除最后一个节点以外的剩余节点的倒序，也不应该是null啊。

#### 比如：`return pre`就应该是`5->4->3->2->1->null`的话，`return pre.next`就应该是`4->3->2->1->null`。



个人觉得很有意思，回去后和室友讨论了一下，觉得确实有点问题，把问题跟`leetcode`反馈了一下，目前还没有回复。

![image-20231229111250616](https://real-jack.oss-cn-beijing.aliyuncs.com/undefinedimage-20231229111250616.png)



### <span style="background:#eef0f4;color:red">事情更新一下，初步的怀疑是因为leetcode的检查机制是重新一路next返回整个链表，而我返回的`pre.next`最终会在头结点处返回空值`null`，这样就能解释了。</span>

附上代码随想录的反转链表过程示意图（画的太漂亮了）：

![206.翻转链表](https://real-jack.oss-cn-beijing.aliyuncs.com/undefined206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.gif)
