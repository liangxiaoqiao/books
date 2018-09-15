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

##### TensorFlow数据模型——张量（tensor）

1. 张量是tensorflow管理数据的形式
2. 从功能角度上，张量可以简单的被理解为多维数组。
3. 张量中并没有真正保存数字，它保存的是如何得到这些数字的计算过程。
4. 张量中主要保存了三个属性：**名字，维度，类型**。
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
   
   # 自动将生成的会话注册为默认会话
   session= tf.InteractiveSession()
   ```


##### TensorFlow实现神经网络

1. 提取特征向量对机器学习的效果至关重要。

2. 神经网络解决分类问题：

   1. 提取问题中的特征向量作为神经网络的输入
   2. 定义神经网络的结构，并定义如何从神经网络的输入得到输出（也就是神经网络的前向传播算法）
   3. 通过训练数据来调整神经网络中的参数的取值
   4. 使用训练好的神经网络来预测未知的数据

3. 神经元是构成一个神经网络的最小单元

   ```markdown
   一个神经元有多个输入和一个输出。
   神经元的输入既可以是其他神经元的输出，也可以是整个神经网络的输入。
   神经网络的结构指的是不同神经元之间的连接结构。
   一个最简单的神经元的输出就是所有输入的 加权和，而不同输入的权重就是神经元的参数。
   神经网络的优化过程就是优化神经元中参数取值的过程。
   ```

4. 简单的神经网络前向传播算法

   ````python
   # 测试前向传播算法
   def test_forward():
       # 原始输入值
       ori = tf.constant([[0.7, 0.9]], name="Origin")
       # 也可以使用tensorflow的随机数生成函数
       # 第一层网络
       level_first = tf.Variable(tf.constant([[0.2, 0.1, 0.4], [0.3, -0.5, 0.2]], name="Level_1"))
       # 第二层网络
       level_two = tf.Variable(tf.constant([[0.6], [0.1], [-0.2]], name="Level_2"))
       with tf.Session() as sess:
           # 多个变量，这里直接初始化所有变量
           # 替代下边的一个一个初始化变量
           # init = tf.global_variables_initializer()
           # sess.run(init)
           result_1 = tf.matmul(ori, level_first)
           result_2 = tf.matmul(result_1, level_two)
           # 初始化变量 第一层网络
           sess.run(level_first.initializer)
           # 初始化变量 第二层网络
           sess.run(level_two.initializer)
           r1 = sess.run(result_1)
           r2 = sess.run(result_2)
           print(r1)
           print(r2)
   ````

5. placeholder机制用于提供输入数据，placeholder相当于定义了一个位置，这个位置中的数据在程序运行时再指定。

   ```python
   # 测试placeholder
   def test_placeholder():
       # 也可以使用tensorflow的随机数生成函数
       # # 第一层网络
       # level_one = tf.Variable(tf.constant([[0.2, 0.1, 0.4], [0.3, -0.5, 0.2]], name="Level_1"))
       # # 第二层网络
       # level_two = tf.Variable(tf.constant([[0.6], [0.1], [-0.2]], name="Level_2"))
       level_one = tf.Variable(tf.random_normal([2, 3], stddev=1, seed=1))
       level_two = tf.Variable(tf.random_normal([3, 1], stddev=1, seed=1))
       # 定义输入数据
       place_holder = tf.placeholder(tf.float32, shape=(3, 2), name="input")
       with tf.Session() as sess:
           # 多个变量，这里直接初始化所有变量
           # 替代下边的一个一个初始化变量
           init = tf.global_variables_initializer()
           sess.run(init)
           result_1 = tf.matmul(place_holder, level_one)
           result_2 = tf.matmul(result_1, level_two)
           # 相当于定义了三组输入数据
           r2 = sess.run(result_2, feed_dict={place_holder: [[0.7, 0.9], [0.1, 0.4], [0.5, 0.8]]})
           print(r2)
   ```

   

