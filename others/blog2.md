#### 什么是回溯法？
什么是回溯法，以及回溯法的设计过程，和回溯法的经典应用“八皇后问题”，请参考我的另一篇文章，这篇只是用来讲解回溯法的另一种应用，数独问题。
##### [回溯法之八皇后问题]()

#### 什么是数独？
    ```
    数独是源自18世纪瑞士的一种数学游戏。是一种运用纸、笔进行演算的逻辑游戏。玩家需要根据9×9盘面上的已知数字，推理出所有剩余空格的数字，并满足每一行、每一列、每一个粗线宫（3*3）内的数字均含1-9，不重复。
    ```

##### 最难数独：
![来自百度百科](https://github.com/liangxiaoqiao/images/raw/develop/blog/backtracing/sudoku.jpg)

#### 数独问题的代码步骤：
1. 从做到右开始检查每一个没有填值的空格
2. 在第一个空格放置从1到9放置数字，检查是否可以放在这个位置
3. 可以，则继续放置下一个空位，否则，退回去，更换第一个空格的数字。
4. 直到放置完所有空格

###### Talk is cheap, show me the code.
1. 创建对象，初始化数独
```java
public class Sudoku {
    private int[][] metrics;

    public Sudoku(int[][] metrics) {
        this.metrics = metrics;
    }
}
```
2. 放置数字
``` java

    public void backTrace(int i, int j) {
        // 最后一个位置了，那么找到了一个解
        if (i == 8 && j == 9) {
            print(metrics);
            return;
        }

        // 当前放置第i行的第10个数字，那么需要换行了
        if (j > 8) {
            i = i + 1;
            j = 0;
        }

        //如果是0，说明需要放置一个数字，不是0 继续放置下一个位置
        if (metrics[i][j] == 0) {
            for (int k = 1; k <= 9; k++) {
                metrics[i][j] = k;
                if (check(i, j, k)) {
                    check(i, j, k);
                    backTrace(i, j + 1);
                }
                metrics[i][j] = 0;
            }
        } else {
            backTrace(i, j + 1);
        }
    }
```

3. 检查数字是否满足要求
```java
    //检查的时候把行 列 方块，都看做了一个四个坐标定位的二维数组
    //（这里完全可以遍历循环，不要这样写，虽然看着简洁，影响理解）
    private boolean check(int row, int col, int number) {
        //检查行
        int rowStartX = row, rowStartY = 0, rowEndX = row, rowEndY = 8;
        //检查列
        int colStartX = 0, colEndX = 8, colStartY = col, colEndY = col;
        //检查方块
        int x = row / 3, y = col / 3, mStartX = 3 * x, mStartY = 3 * y, mEndX = mStartX + 2, mEndY = mStartY + 2;

        return !(hasNumber(rowStartX, rowStartY, rowEndX, rowEndY, row, col, number)
                || hasNumber(colStartX, colStartY, colEndX, colEndY, row, col, number)
                || hasNumber(mStartX, mStartY, mEndX, mEndY, row, col, number));
    }

    //检查的时候 要排除掉 当前位置的数字。
    private boolean hasNumber(int startX, int startY, int endX, int endY, int row, int col, int number) {
        for (int x = startX; x <= endX; x++) {
            for (int y = startY; y <= endY; y++) {
                if (x == row && y == col) {
                    continue;
                }
                if (metrics[x][y] == number) {
                    return true;
                }
            }
        }
        return false;
    }
```

至此，代码已经结束了。代码只是为了熟悉回溯法的解题步骤，所以并没有做太多的优化。  
回溯法的对比循环的好处就在于，减少了很多不必要的循环。  
本例中，可以看到当前边位置的数字不合适，那么后边的不论你怎么放，都是不合适的，所以减少了很多次的循环。
同时，本例中放置数字时选择的策略为从1-9依次放入，其实可以优化可以防止的数字，也可以优化检查的方法，本例并不是讲解回溯法的优化，所以不在深入讲解。

#### 完整代码如下(可直接运行):
```java
public class Sudoku {
    private int[][] metrics;

    public Sudoku(int[][] metrics) {
        this.metrics = metrics;
    }


    public void backTrace(int i, int j) {
        // 最后一个位置了，那么找到了一个解
        if (i == 8 && j == 9) {
            print(metrics);
            return;
        }

        // 当前放置第i行的第10个数字，那么需要换行了
        if (j > 8) {
            i = i + 1;
            j = 0;
        }

        //如果是0，说明需要放置一个数字，不是0 继续放置下一个位置
        if (metrics[i][j] == 0) {
            for (int k = 1; k <= 9; k++) {
                metrics[i][j] = k;
                if (check(i, j, k)) {
                    check(i, j, k);
                    backTrace(i, j + 1);
                }
                metrics[i][j] = 0;
            }
        } else {
            backTrace(i, j + 1);
        }
    }


    //检查的时候把行 列 方块，都看做了一个四个坐标定位的二维数组
    //（这里完全可以遍历循环，不要这样写，虽然看着简洁，影响理解）
    private boolean check(int row, int col, int number) {
        //检查行
        int rowStartX = row, rowStartY = 0, rowEndX = row, rowEndY = 8;
        //检查列
        int colStartX = 0, colEndX = 8, colStartY = col, colEndY = col;
        //检查方块
        int x = row / 3, y = col / 3, mStartX = 3 * x, mStartY = 3 * y, mEndX = mStartX + 2, mEndY = mStartY + 2;

        return !(hasNumber(rowStartX, rowStartY, rowEndX, rowEndY, row, col, number)
                || hasNumber(colStartX, colStartY, colEndX, colEndY, row, col, number)
                || hasNumber(mStartX, mStartY, mEndX, mEndY, row, col, number));
    }

    //检查的时候 要排除掉 当前位置的数字。
    private boolean hasNumber(int startX, int startY, int endX, int endY, int row, int col, int number) {
        for (int x = startX; x <= endX; x++) {
            for (int y = startY; y <= endY; y++) {
                if (x == row && y == col) {
                    continue;
                }
                if (metrics[x][y] == number) {
                    return true;
                }
            }
        }
        return false;
    }


    private void print(int[][] metrics) {
        for (int i = 0; i < metrics.length; i++) {
            System.out.println(Arrays.toString(metrics[i]));
        }
        System.out.println("================");
    }

    public static void main(String[] args) {


        int[][] metrics = {
                {0, 0, 5, 3, 0, 0, 0, 0, 0},
                {8, 0, 0, 0, 0, 0, 0, 2, 0},
                {0, 7, 0, 0, 1, 0, 5, 0, 0},
                {4, 0, 0, 0, 0, 5, 3, 0, 0},
                {0, 1, 0, 0, 7, 0, 0, 0, 6},
                {0, 0, 3, 2, 0, 0, 0, 8, 0},
                {0, 6, 0, 5, 0, 0, 0, 0, 9},
                {0, 0, 4, 0, 0, 0, 0, 3, 0},
                {0, 0, 0, 0, 0, 9, 7, 0, 0}
        };

        Sudoku sudoku = new Sudoku(metrics);
        long start = Instant.now().toEpochMilli();
        sudoku.backTrace(0, 0);
        long end = Instant.now().toEpochMilli();
        System.out.println("耗时(ms)：" + (end - start));

    }
}
```