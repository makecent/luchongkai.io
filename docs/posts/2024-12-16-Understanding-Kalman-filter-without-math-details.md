---
title: "Understanding Kalman filter without math details"
parent: Posts
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# Introduction
{: .no_toc }
This post show how I understand the Kalman filter after learning some tutorials. Only the conception equations are introduced.

# 基本问题
## 什么是卡尔曼滤波？
它是一种思想（而非具体算法），**用一个变量的过去值和现在的观测值，来最佳估计变量的现在的值**。它有许多不同的具体算法形式，被广泛应用于信号处理、数据融合、运动估计、自动控制等领域。

## 什么时候使用卡尔曼滤波？
卡尔曼滤波应用场景的基础假设是：
1. 我们有一个方法来**观测**变量**现在的值**。
2. 我们同时也可以用变量的**过去的值**来**预测**它**现在的值**。

在一般应用中，我们常常直接使用假设1。但是如果假设2成立的话，我们就会想：不把假设2利用起来实在太可惜了。数学上也有严格证明，**结合**这两个假设的结果，肯定比单独使用一个要好。卡尔曼滤波正是使用在这种场景中。

相应的，不适用于卡尔曼滤波的场景就是：这个变量不存在时序结构。或者说，即便存在时序结构，它的某个时刻的状态与它之前的状态毫无关系，那么假设1便不成立。

## 为什么叫“滤波”
上面的说明中，**滤波**的操作其实已经出现了：把一个变量的观测值，按时间排序形成一个一维的矩阵，用一个滤波器在这个矩阵上从左到右滑动，来对这个序列进行滤波，更新观测值。
假设这个滤波器为[0.3, 0.7, 0.0]，就意味着对于每个观测值，我们都用其（前一个状态的30% + 观测到的值的70% + 下一个状态的0%）来更新这个观测值，这反映的正是卡尔曼滤波的思想。


# 简单理解
![image](https://github.com/user-attachments/assets/cc11f975-c21f-462a-947c-a97002a55f46)

![image](https://github.com/user-attachments/assets/5ee1c3ff-99c5-480a-8085-c839c2c466df)

