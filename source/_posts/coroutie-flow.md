---
title: coroutie-flow
date: 2022-03-20 20:46:54
tags: coroutie
categories: Kotlin
---



### 56Flow 异步流

![2022-03-20_8.47.50](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_8.47.50.png)



##### 异步返回多个值的方案

集合 , 序列 , 挂起函数 ,Flow



##### 如何表示多个值

![2022-03-20_8.49.02](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_8.49.02.png)

![2022-03-20_8.58.42](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_8.58.42.png)

![2022-03-20_9.00.07](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.00.07.png)

##### 通过Flow异步返回多个值

  

**可以去掉suspend**

![2022-03-20_9.02.24](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.02.24.png)

![2022-03-20_9.03.12](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.03.12.png)

再起一个任务，确认线程是否阻塞

![2022-03-20_9.04.46](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.04.46.png)



##### Flow与其他方式的区别

![2022-03-20_9.06.40](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.06.40.png)

##### Flow应用

![2022-03-20_9.09.34](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.09.34.png)

### 流的特性

##### 60 冷流

![2022-03-20_9.12.12](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_9.12.12.png)

类似于懒加载



61.流的连续性



![2022-03-20_10.09.29](/Users/m/Documents/BLOG/source/_posts/coroutie-flow/2022-03-20_10.09.29.png)




