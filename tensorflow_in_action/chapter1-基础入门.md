#### 基本概念

##### TensorFlow计算模型——计算图

1. 计算图是tensorflow中最基本的一个概念。

2. tensorflow中的所有计算都会被转化为计算图上的节点

3. tensorflow中，张量可以被简单的理解为多维数组

4. flow体现了它的计算模型，直观的表达了张量之间通过计算相互转化的过程。

5. tensorflow是一个通过计算图的形式来表述计算的编程系统

6. tensorflow中的每一个计算都是计算图上的一个节点，而节点之间的边描述了计算之间的依赖关系。

7. tensorflow程序一般可以分为两个阶段：**1. 在第一个阶段 需要定义计算图中所有的计算 2. 第二个阶段为执行计算**

   ```python
   import tensorflow as tf
   a = tf.constant([1,2], name="a")
   a = tf.constant([2,3], name="b")
   result = a+b
   ```

8. 在tensorflow程序中，系统会自动维护一个默认的计算图。支持通过tf.Graph()函数来生成新的计算图。不同计算图上的张量和运算都不会共享。

##### TensorFlow数据模型——张量

1. 张量是tensorflow管理数据的形式
2. 从功能角度上，张量可以简单的被理解为多维数组。
3. 张量中并没有真正保存数字，它保存的是如何得到这些数字的计算过程。
4. 张量中主要保存了三个属性：名字，维度，类型。
5. 张量的使用：
   1. 对中间计算结果的引用 
   2. 当计算图构造完成之后，张量可以用来获得计算结果。

##### TensorFlow运行模型——会话

1. tensorflow中的会话来执行定义好的运算

2. 所有计算完成之后需要关闭会话来帮助系统回收资源。

   ```python
   # 创建一个会话
   sess = tf.Session()
   # 执行计算
   sess.run(...)
   # 关闭会话，释放资源
   sess.close()
   
   # 为了解决异常退出时资源释放问题，可以通过python的上下文管理器来使用会话
   with tf.Session() as sess:
   	sess.run(...)
   ```

3. 设置默认会话

   ```
   sess = tf.Session()
   with sess.as_default():
   	print(result.eval())
   
   # 以下代码也可实现，以下两个命令具有相同的功能
   sess = tf.Session()
   sess.run(result)
   result.eval(session=sess)
   
   ```

   