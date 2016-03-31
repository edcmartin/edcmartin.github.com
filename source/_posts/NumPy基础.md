title: NumPy基础
date: 2016-02-10 14:46:53
tags:
- Python
- NumPy
---
NumPy ( Numerical Python的简称 ) 是高性能科学计算和数据分析的基础包

### 0. Numpy 文档
On the web: <http://docs.scipy.org/>
帮助

    np.array?
<!--more-->
### 1. 导入numpy
    import numpy as np

### 2. 创建ndarry

+ 使用array函数
```python
import numpy as np
data = [6, 7.5, 8, 0, 1] 
arr = np.array(data) #接受一切序列的对象
arr
Out[1]: array([ 6. ,  7.5,  8. ,  0. ,  1. ])
```
+ 生成多维数组
```python
data2 = [[1, 2, 3], [4, 5, 6]] #二维的列表
arr2 = np.array(data2)
arr2
Out[1]: 
array([[1, 2, 3],
       [4, 5, 6]])
arr2.ndim #array的维数
Out[2]: 2
arr2.shape #形状
Out[3]: (2,3)
```
+ 函数创建数组
```
np.zeros(5)
Out[1]: array([ 0.,  0.,  0.,  0.,  0.])
np.ones((2,3))
Out[2]: 
array([[ 1.,  1.,  1.],
       [ 1.,  1.,  1.]])

np.empty((2,3,2))

np.arange(7) #和range函数类似
Out[3]: array([0, 1, 2, 3, 4, 5, 6])
np.linspace(0, 1, 6) #平均分成五份
Out[4]: array([ 0. ,  0.2,  0.4,  0.6,  0.8,  1. ])
np.linspace(0, 1, 5, endpoint=False)
Out[5]: array([ 0. ,  0.2,  0.4,  0.6,  0.8])

np.eye(2)
Out[6]: 
array([[ 1.,  0.],
       [ 0.,  1.]])

np.random.rand(4) # uniform in [0, 1] 均匀分布
Out[7]: array([ 0.88479646,  0.07842514,  0.56394621,  0.80994074])
np.random.randn(4) # Gaussian 高斯分布
Out[8]: array([ 1.211699  ,  1.02448625,  0.86236071,  1.34949778])
```
### 3. 数据类型
array会自动匹配数组的数据类型
指定数据类型
```python
c = np.array([1, 2, 3], dtype=float) #指定了数组数据的类型
c.dtype
Out[1]: dtype('float64')

a = np.ones((3, 3))  #默认数据类型为float64
a.dtype
Out[23]: dtype('float64')
```
其他还有负数，布尔值，字符串，整型
注：如果没有特别指定，数据类型基本都是float64（浮点数)

### 4. 可视化
Matplotlib 是用来做2D图的包

    import matplotlib.pyplot as plt #常用的导入方式
可以使用下面的函数来显示图像

    plt.plot(x, y)
    plt.show()
##### 举例
```python
x = np.linspace(0,3,20)
y = np.linspace(0,4,20)
plt.plot(x, y) #画线
plt.plot(x, y, 'o') #画点
```