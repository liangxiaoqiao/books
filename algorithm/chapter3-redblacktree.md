## 红黑树

---

### 定义：

```
1. 节点是红色或者是黑色；
2. 根节点是黑色；
3. 每个叶节点（叶子节点也就是 NIL或空节点）是黑色;
4. 每个红色节点的两个子节点都是黑色的（也就是说不存在两个连续的红色节点）；
5. 从任一节点到其没个叶节点的所有路径都包含相同数目的黑色节点;
```
---

### 左旋 与 右旋:

---

### 插入操作:
#### 插入规则：
    父节点F 叔叔节点U 祖父节点G
1. 插入的是根节点，染黑，结束
1. 插入的节点 父节点 是黑色，直接结束
1. 插入的节点 父节点是红色，叔叔节点也是红色
    1. 父节点 叔叔节点 染黑，祖父节点染红
    1. 递归处理祖父节点
1. 插入的节点 父节点是红色，叔叔节点是黑色

    1. 父节点 是 祖父节点 左儿子
        1. 新节点 是父节点左儿子：祖父节点G右旋 G染黑，F染红
        1. 新节点 是父节点右儿子：新节点的父节点左旋，新节点的新父节点右旋 新节点黑 新父节点 红（交换颜色）

    1. 父节点 是 祖父节点 右儿子
        1. 新节点 是父节点左儿子：新节点的父节点右旋，新节点的新父节点左旋  新节点黑 新父节点 红（交换颜色）
        1. 新节点 是父节点右儿子：祖父节点G左旋，父黑 祖父红
--- 

### 删除操作：
#### 删除规则：

```
我们只需要讨论删除只有一个儿子的节点（如果它两个儿子都为空，即均为叶子，我们任意将其中一个看作它的儿子）。
```
1. 删除的节点是红色（它的父亲儿子一定是黑色的），所以可以简单的用他的黑色儿子替换它。
1. 删除的节点是黑色，而它的儿子是红色的时候。红色儿子顶上来破坏性质5，所以将它涂为黑色。


1. **删除的节点是黑色，儿子也是黑色的情况：** 
    ```
    我们首先把要删除的节点替换为它的儿子。出于方便，
    N:称呼这个儿子为N（在新的位置上），
    S:称呼它的兄弟（它父亲的另一个儿子）为S。
    在下面的示意图中，我们还是使用P称呼N的父亲，SL称呼S的左儿子，SR称呼S的右儿子。
    ```
    
    1.  情形1：N是新的根。在这种情形下，我们就做完了。我们从所有路径去除了一个黑色节点，而新根是黑色的，所以性质都保持着。

    1.  情形2：S是红色。
        
        ```
        在这种情形下我们在N的父亲上做左旋转，把红色兄弟转换成N的祖父，我们接着对调N的父亲和祖父的颜色。完成这两个操作后，尽管所有路径上黑色节点的数目没有改变，但现在N有了一个黑色的兄弟和一个红色的父亲（它的新兄弟是黑色因为它是红色S的一个儿子），所以我们可以接下去按情形4、情形5或情形6来处理。
        ```
        * 对调N的父亲和S的颜色
        * N的父亲进行左旋
        * 按照情形4、情形5或情形6来处理

    1.  情形3： N的父亲、S和S的儿子都是黑色的。
        
        ```
        在这种情形下，我们简单的重绘S为红色。结果是通过S的所有路径，它们就是以前不通过N的那些路径，都少了一个黑色节点。因为删除N的初始的父亲使通过N的所有路径少了一个黑色节点，这使事情都平衡了起来。但是，通过P的所有路径现在比不通过P的路径少了一个黑色节点，所以仍然违反性质5。要修正这个问题，我们要从情形1开始，在P上做重新平衡处理。
        ```
        * S绘制为红色
        * 从情形1开始，在P上做重新平衡处理

    1.  情形4：

        ```
         S和S的儿子都是黑色，但是N的父亲是红色。在这种情形下，我们简单的交换N的兄弟和父亲的颜色。这不影响不通过N的路径的黑色节点的数目，但是它在通过N的路径上对黑色节点数目增加了一，添补了在这些路径上删除的黑色节点。
        ```
        * 交换N的父亲和S的颜色

    1.  情形5：
        
        ```
        S是黑色，S的左儿子是红色，S的右儿子是黑色，而N是它父亲的左儿子。在这种情形下我们在S上做右旋转，这样S的左儿子成为S的父亲和N的新兄弟。我们接着交换S和它的新父亲的颜色。所有路径仍有同样数目的黑色节点，但是现在N有了一个黑色兄弟，他的右儿子是红色的，所以我们进入了情形6。N和它的父亲都不受这个变换的影响。
        ```

        * S右旋转
        * 交换S和他的新父亲的颜色

    1.  情形6：

        ```
        S是黑色，S的右儿子是红色，而N是它父亲的左儿子。在这种情形下我们在N的父亲上做左旋转，这样S成为N的父亲（P）和S的右儿子的父亲。我们接着交换N的父亲和S的颜色，并使S的右儿子为黑色。子树在它的根上的仍是同样的颜色，所以性质3没有被违反。但是，N现在增加了一个黑色祖先：要么N的父亲变成黑色，要么它是黑色而S被增加为一个黑色祖父。所以，通过N的路径都增加了一个黑色节点。
        此时，如果一个路径不通过N，则有两种可能性：
        它通过N的新兄弟。那么它以前和现在都必定通过S和N的父亲，而它们只是交换了颜色。所以路径保持了同样数目的黑色节点。
        它通过N的新叔父，S的右儿子。那么它以前通过S、S的父亲和S的右儿子，但是现在只通过S，它被假定为它以前的父亲的颜色，和S的右儿子，它被从红色改变为黑色。合成效果是这个路径通过了同样数目的黑色节点。
        在任何情况下，在这些路径上的黑色节点数目都没有改变。所以我们恢复了性质4。在示意图中的白色节点可以是红色或黑色，但是在变换前后都必须指定相同的颜色。
        ```
        *  N的父亲左旋
        *  交换N的父亲和S的颜色
        *  S的右儿子为黑色