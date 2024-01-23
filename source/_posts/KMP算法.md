---
title: KMP算法
categories: 个人学习
tags:
  - 学习
  - Java
description: java中KMP算法的使用
abbrlink: 2da0528d
date: 2023-12-27 14:59:06
keywords:
---

学习一下KMP算法和在Java中的使用。
<!-- more -->



### <span style="background:#eef0f4;color:blue">什么是KMP算法</span>

因为是由这三位学者发明的：Knuth，Morris和Pratt，所以取了三位学者名字的首字母。所以叫做KMP

### <span style="background:#eef0f4;color:blue">前缀表</span>

作用：避免重复匹配

首先要知道前缀表的任务是当前位置匹配失败，找到之前已经匹配上的位置，再重新匹配，此也意味着在某个字符失配时，前缀表会告诉你下一步匹配中，模式串应该跳到哪个位置。

字符串的前缀是指**不包含最后一个字符**的所有以**第一个字符开头**的连续子串；
字符串的后缀是指**不包含第一个字符**的所有以**最后一个字符结尾**的连续子串。

那么什么是前缀表：**<span style="color:red">记录下标i之前（包括i）的字符串中，有多大长度的相同前缀后缀。</span>**



**获取前缀表：**

在实际编码时，通常我会往原串和匹配串头部追加一个空格（哨兵）。

目的是让 `j` 下标从 `0` 开始，省去 `j` 从 `-1` 开始的麻烦。

```
private void getNext(int[] next, String s) {
    int j = 0;
    next[0] = 0;
    for (int i = 1; i < s.length(); i++) {
        while (j > 0 && s.charAt(j) != s.charAt(i)) 
            j = next[j - 1];
        if (s.charAt(j) == s.charAt(i)) 
            j++;
        next[i] = j; 
    }
}
```

**图片示意：**

![6127EBA37435560C20BB8B15D5B790B6.png](https://real-jack.oss-cn-beijing.aliyuncs.com/undefined1618847995-vRWimV-6127EBA37435560C20BB8B15D5B790B6.png)



**题目：**

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回 -1。



**完整代码：**



```Java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.length() == 0) return 0;
        int[] next = new int[needle.length()];
        getNext(next, needle);

        int j = 0;
        for (int i = 0; i < haystack.length(); i++) {
            while (j > 0 && needle.charAt(j) != haystack.charAt(i)) 
                j = next[j - 1];
            if (needle.charAt(j) == haystack.charAt(i)) 
                j++;
            if (j == needle.length()) 
                return i - needle.length() + 1;
        }
        return -1;

    }
    
    private void getNext(int[] next, String s) {
        int j = 0;
        next[0] = 0;
        for (int i = 1; i < s.length(); i++) {
            while (j > 0 && s.charAt(j) != s.charAt(i)) 
                j = next[j - 1];
            if (s.charAt(j) == s.charAt(i)) 
                j++;
            next[i] = j; 
        }
    }
}
```





