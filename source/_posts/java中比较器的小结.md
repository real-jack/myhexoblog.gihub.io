---

title: java中比较器的小结
categories: 个人学习
tags: [Java, 学习]
description: leetcode遇见了PriorityQueue的比较器，好久没写有些忘了，复习一下。
abbrlink: 4e5abcb0
date: 2024-01-08 16:35:22
keywords:
---

<font face="楷体" size=8><span style="background:#eef0f4;color:DodgerBlue">前情回顾：</span></font>

`leetcode`遇见了`PriorityQueue`的比较器，好久没写有些忘了，复习一下。



<font face="楷体" size=8><span style="background:#eef0f4;color:DodgerBlue">主要涉及的代码：</span></font>

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<Integer,Integer>();
        for(Integer i:nums){
            map.put(i, map.getOrDefault(i,0)+1);
        }
        Queue<Integer> pq = new PriorityQueue(new Comparator<Integer>(){
            @Override
            public int compare(Integer e1,Integer e2){
                return map.get(e2)-map.get(e1);
            }
        });
        for(Integer key:map.keySet()){
            pq.add(key);
        }
        int[] res = new int[k];
        for(int i=0;i<k;++i){
            res[i] = pq.remove();
        }
        return res;
    }
}
```



改为`lambda`表达式：

```
PriorityQueue<Integer> pq = new PriorityQueue((e1, e2) -> map.get(e2) - map.get(e1));
```

### <font face = "华文彩云" color="MediumOrchid">这代码，优雅，实在是太优雅了！</font>

<div style="position: relative; width: 100%; height: 0; padding-bottom: 75%;">
    <iframe src="//player.bilibili.com/player.html?bvid=BV1yA4y1D7zV"  scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="position: absolute; width: 100%; height: 100%; left: 15%; top: 0;"></iframe>
</div>









<font face="楷体" size=8><span style="background:#eef0f4;color:DodgerBlue">比较器的升降序：</span></font>

```java
//升序
return e1-e2;
```

与

```java
//降序
return e2-e1;
```

规则是`return`的`<0`就顺序不变，`>0`就交换。

所以，怎么判断就很一目了然了。



![《哔哩哔哩》优雅实在太优雅了梗的意思介绍](https://real-jack.oss-cn-beijing.aliyuncs.com/undefined1669384306.gif)



ps：还是放一张图片比较简单：）
