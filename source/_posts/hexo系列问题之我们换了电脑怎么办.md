---
title: hexo系列问题之我们换了电脑怎么办
categories: 个人学习
tags:
  - hexo
  - 学习
description: 学习一下换电脑了，hexo怎么修改
abbrlink: 413c7e08
date: 2023-12-25 17:00:53
keywords:
---

学习一下换电脑了，hexo怎么修改
<!-- more -->

#### 参考的播主：[http://www.xiaolongwu.cn](http://www.xiaolongwu.cn)


这个问题是我刚开始建站的时候就想到的问题，只是一直没时间做这些，最近有点时间了，处理一下这个问题
#### 问题
我们如果换了电脑怎么办？我们把hexo文件从一个电脑cope到另外一个电脑吗?答案肯定不是这样的，因为这里面有好多依赖包，好几万个文件呢，这样显然不合理
#### 解决方案
我们初步的解决方案是把我们的文件提交到git上，利用git来管理它，我是这样解决的
1. 在现有的XXX.github.io项目上创建一个分支来管理

2. 具体实现步骤：
    1. 克隆gitHub上的XXX.github.io项目的文件到本地
    
    ``` bash
    git clone https://github.com/yourname/xxx.github.io.git
    ```
    
    2. 删除文件夹里除了.git的其他所有文件
    3. 把hexo项目文件下的所有文件全部复制过来
    4. 里面应该有一个叫.gitignore的文件，如果没有就输入 touch .gitignore，创建一个
    5. .gitignore文件里应该是这些内容
        ``` bash
        .DS_Store 
        Thumbs.db 
        db.json 
        *.log
        node_modules/ 
        public/ 
        .deploy*/ 
        ```
    6. 创建一个叫hexo的分支并切换到这个分支上
    ``` bash
    git checkout -b hexo
    ```
    7. 提交复制过来的文件到暂存区
    ``` bash
    git add --all
    ```
    
    8. 提交 
      ``` bash
      git commit -m "新建分支资源文件"
      ```
    
    9. 推送分支到github
    ``` bash
    git push --set-upstream origin hexo
    ```
    
    到这一步我们就基本上搞定了，以后再跟新了博客就直接 git push就可以了，hexo的操作跟以前一样不变。
3. 今后无论什么时候想要在其他电脑上面用hexo写博客，就直接把创建的分支克隆下来，npm install安装依赖之后就可以用了。
``` bash
//克隆分支的操作 

git clone -b hexo https://github.com/yourname/xxx.github.io.git  
```
4. 因为上面创建的是一个名字叫hexo的分支，所以这里-b后面的是hexo，再把后面的gitHub的地址换成你自己的hexo博客的地址就可以了。
5. 这样做完了以后，每次写完博客发布之后不要忘了还要git push把源文件推到分支上。

**我的个人博客：[https://real-jack.github.io](https://real-jack.github.io)**



{% codeblock %}
alert('Hello World!');
alert('Hello World!');
alert('Hello World!');
{% endcodeblock %}



