#### 深层神经网络

```
进一步介绍如何设计和优化神经网络，使它能够更好地对未知的样本进行预测。
```

##### 深度学习与深层神经网络

1. 深度学习：“一类通过多层非线性变幻对搞复杂性数据建模算法的合集。”

   ```
   因为深层神经网络是实现“多层非线性变幻”最常用的一种方法，所以实际中基本上可以认为深度学习就是深层神经网络的代名词。
   ```

2. 深度学习有两个非常重要的特性——多层和非线性。

3. 线性模型的局限性

   1. 在线性模型中，模型的输出为输入的加权和。

   2. 线性模型的最大特点就是任意线性模型的组合仍然还是线性模型。

   3. 上一章的前向传播算法实现就是一个线性模型。虽然这个神经网络有两层，但是他和单层的神经网络并没有区别。

      ```
      根据矩阵乘法的结合律，a1 = x*w1, y = a1*w2，得到 y = x*(w1*w2)，也就是 y= xw'。
      只通过线性变换，任意层的全连接神经网络和单层神经网络模型的表达能力没有任何区别，而且他们都是线性模型。
      ```

   4. 线性模型能够解决的问题是有限的

   5. 一个问题可以通过一条直线来划分，那么线性模型就可以用来解决这个问题。

4. 激活函数实现去线性化

   1. 第一个改变：新的公式中增加了偏置项（bias）
   2. 第二个改变：每个节点的取值不再是单纯的加权和。

5. 多层网络可以解决异或运算

6. 损失函数

   1. 分类问题

      ```
      判断零件合格不合格是一个二分类问题。判断手写数字可以归纳为十分类问题。

      解决二分类问题：设置一个阈值。（节点输出越接近0，越有可能是不合格的。越接近1，越有可能是合格的。所以可以设置阈值为0.5，区分合格与不合格。）
      解决多分类问题最常用的方法是设置n个输出节点。对于每一个样例，得到一个n维数组，对应k上的节点输出值应为1，其它节点为0.（如何判断向量和期望的向量有多接近呢？ 交叉熵是常用的评判方法之一。）
      ```

   2. 交叉熵 刻画了两个概率分部之间的距离，他是分类问题中使用比较广的一种损失函数。

   3. Softmax回归将神经网络的输出变成一个概率分布。

      ```python
      cross_entropy = -tf.reduce_mean(
      	y_ * tf.log(tf.clip_by_value(y,1e-10,1.0)))
      # y_代表正确结果，y 代表预测结果

      ```

7. 自定义损失函数

   ```python
   def test_custom_func():
       """
       1. 定义输入节点
       2. 定义神经网络传播过程
       3. 定义运算
       4. 定义损失函数
       5. 训练步骤
       6. 训练
       :return:
       """
       batch_size = 8
       STEPS = 5000
       data_size = 128
       # 1.定义输入节点
       x = tf.placeholder(tf.float32, shape=(None, 2), name="x-input")
       y_ = tf.placeholder(tf.float32, shape=(None, 1), name="y-input")  # y_是神经网络预测值
       # 2.定义神经网络传播过程
       w1 = tf.Variable(tf.random_normal([2, 1], stddev=1, seed=1))
       # 3.定义运算
       y = tf.matmul(x, w1)  #

       # 4. 定义损失函数
       loss_less = 10
       loss_more = 1
       loss = tf.reduce_mean(tf.where(tf.greater(y, y_), (y - y_) * loss_more, (y_ - y) * loss_less))
       train_step = tf.train.AdamOptimizer(0.001).minimize(loss)

       # 模拟数据集
       rdm = RandomState(1)
       X = rdm.rand(data_size, 2)
       Y = [[x1 + x2 + rdm.rand() / 10.0 - 0.05] for (x1, x2) in X]

       # 5.训练步骤
       with tf.Session() as sess:
           init_op = tf.global_variables_initializer()
           sess.run(init_op)
           # 6.开始训练
           for i in range(STEPS):
               start = (i * batch_size) % data_size
               end = min(start + batch_size, data_size)
               sess.run(train_step, feed_dict={x: X[start: end], y_: Y[start: end]})
               print(sess.run(w1))
   ```

8. 梯度下降算法的缺点：1并不能保证被优化的函数打到全局最优解。2.计算时间太长。

9. 为了综合梯度下降算法和随机梯度下降算法的优缺点：每次计算一小部分训练数据的损失函数。
