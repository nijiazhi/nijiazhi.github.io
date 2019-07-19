---
layout: post
title: Eigen矩阵运算开源库
categories: [Programming Tools]
tags: Eigen
---

### Index
<!-- TOC -->
- [常见命令](#常见命令)
<!-- /TOC -->

---
## 常用矩阵
```
MatrixXf::Zero(3,4);         // 将矩阵3行4列初始化为0
MatrixXf::Ones(3,3);         // 将矩阵3行3列初始化为1
Vector3f::Ones();            // 将3行的纵向量初始化为1
MatrixXi::Identity(3,3);     //单位阵
Matrix3d::Random();          //随机矩阵

注意：对动态矩阵初始化的时候，必须指定行数和列数。
```

## 矩阵特定初始化
```
m1.setZero();           // 矩阵全部元素置0 
m1.setRandom();         // 随机生成一个矩阵 
m1.setIdentity(3,3);    // 置单位矩阵 
m1.inverse();           // 矩阵求逆 
m1.transpose();         // 矩阵转置 
```


---
# 相关引用
1. [Eigen矩阵运算开源库完全使用指南](https://www.e-learn.cn/content/qita/781840)