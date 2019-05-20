---
layout: post
title:  "Numpy学习笔记 (1)"
date:   2018-12-26 10:30:09 +0900
comments: true
tags:
- python
---

## np.array
- construct ndarray from python array
- ndim: 返回值有几个括弧
- dtype: 也是object，指定ndarray的型, 必须整个数列都是一个型的
```py
a = np.array([1, 2, 3,4,5], ndmin = 2, dtype=complex)
# => [[ 1.+0.j,  2.+0.j,  3.+0.j]]
```

## np.dtype
- `dtype`是object而不是常数
- `np.int32`是type class，和`np.dtype`不同
```py
dt = np.dtype(np.int32)
```

## ndarray.shape
- overwrite shape can reshape the array, reshape后维度不会变， 原来的array会被覆盖
- reshape会返回新的array
```py
a = np.array([[1,2,3],[4,5,6]])
a.shape = (3,2)
b = a.reshape((6, 1))
```

## ndarray.ndim
- 返回维度（int）

## 新建np array
1. np.empty (default dtype float 64)
2. np.ones (default dtype float 64)
3. np.zeros (default dtype float 64)
- shape can be `(1, 2)` or `[1, 2]`
- 如果只指定`int`，默认是`int64`

## 从既存的array创建
- 原来的array和ndarray一定是两个object
1. np.asarray (list or tuple)
- ！⚠️tuple的元素对齐返回值不同
```py
np.asarray(1,2,3),(4,5,6)) #返回二元数组，dtype是int
np.asarray(1,2,3),(4,5)) #返回一元数组，dtype是object
```

## np.arange
- dtype是int，输入float的时候小数点部分会被切掉
- `endpoint=False`会把最后那个数也加进去
```py
np.arange(5, dtype = float)
```

## np.linspace
- `base`是log space的底，default是0（线性）
```py
np.linspace(10,20,5) # 起点，终点，点数
```

## slice
1. use `slice` method
```py
a = np.arange(10)
s = slice(2,7,2)
```
2. [start:stop:step]
```py
a[2:7:2]
```
二元数组的情况下
```py
a = np.array([[1,2,3],[3,4,5],[4,5,6]])
a[1] == a[1, :]
a[:, 1] == a[..., 1] # => True
```
3. boolean slicing
```py
a = np.array([[1,2,3],[3,4,5],[4,5,6]])
a[a > 5] # => 返回一位数组
```

## boradcasting
1. 两个ndarray shape相同时，操作是element-wise
2. 可以boardcast的情况：形状完全相同，形状(n, 1)和(n, m)的情况
