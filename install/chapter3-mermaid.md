####  流程图
##### 1. 各种点的画法

| 表述         | 说明           |
| ------------ | -------------- |
| `id[文字]`   | 矩形节点       |
| `id(文字)`   | 圆角矩形节点   |
| `id((文字))` | 圆形节点       |
| `id>文字]`   | 右向旗帜状节点 |
| `id{文字}`   | 菱形节点       |

```mermaid
graph LR;
node1
node2[node with text]
node3(node with round edges )
node4((node with circle))
node5>node in an asymetric shape]
node6{node text}
node7["This is the (text) in the box"]
A["A double quote:#quot;"] 
B["A dec char:#9829;"]
id1[start with color]
id2[stop with color]
style id1 fill:#f9f,stroke:#333,stroke-width:4px
style id2 fill:#ccf,stroke:#f66,stroke-width:2px,stroke-dasharray: 5, 5

```

##### 2. 各种连线的画法
| 表述       | 说明           |
| ---------- | -------------- |
| `>`        | 添加尾部箭头   |
| `-`        | 不添加尾部箭头 |
| `--`       | 单线           |
| `--text--` | 单线上加文字   |
| `==`       | 粗线           |
| `==text==` | 粗线加文字     |
| `-.-`      | 虚线           |
| `-.text.-` | 虚线加文字     |

```mermaid
graph LR
A1-->B1
A2 --- B2
A11 -.- B11
A3 --添加文字描述 --- B3
A4---|另一种方式|B4
A5-->|带箭头和描述|B5
A6 --另一种带箭头和描述 --> B6
A7-. 虚线描述.- B7
A8-. 虚线描述带箭头 .-> B8
A9 ==> B9
 C1 == 粗线描述==> D1
```

##### 3. 连线方向
| 表述       | 说明           |
| ---------- | -------------- |
| TB      | top bottom 上到下   |
| BT      | bottom top 下到上   |
| LR      | left right 左到右   |
| RL      | right left 右到左  |
| TD      | top down 上到下   |



```mermaid
graph TB
Start-->Stop
```
```mermaid
graph BT
Start-->Stop
```
```mermaid
graph LR
Start-->Stop
```
```mermaid
graph RL
Start-->Stop
```
##### 4. 子图和提示
```mermaid
graph LR
TOTAL-->c1
TOTAL --> a1
TOTAL --> b1

c1-->a2


subgraph one
a1-->a2
end

subgraph two
b1-->b2
end

subgraph three
c1-->c2
end
A[普通提示]
B[链接提示]
A-->B;
click A callback "Tooltip for a callback"
click B "http://www.github.com" "This is a tooltip for a link"
```
#### 时序图
1. 各种例子

| Type | Description                                 |
| ---- | ------------------------------------------- |
| ->   | 实线 没有箭头                   |
| -->  | 虚线 没有箭头                |
| ->>  | 实线 有箭头                  |
| -->> | 虚线 有箭头                  |
| -x   |  实线 箭头 叉号 |
| --x  | 虚线 箭头 叉号 |

```mermaid

sequenceDiagram

    participant A as  Alice
    participant J as  John
    A->>J: Hello John, how are you?
    J->>A: Great!
    A -> J: 实线 没有箭头
    A --> J:虚线 没有箭头
    A ->> J:实线 有箭头
    A -->> J:虚线 有箭头
    A -X J: 实线 箭头 叉号
    A --X J: 虚线 箭头 叉号


    A->>J: Hello John, how are you?(激活 John)
    activate J
    J-->>A: Great! (不激活 Alice)
    deactivate A
    A->>+J: Hello John, how are you?
    J-->>-A : Great!


    A->>+J: Hello John, how are you?
    A->>+J: John, can you hear me?
    A->>+J: John, can you hear me?
    J-->>-A: Hi Alice, I can hear you!
    J-->>-A: Hi Alice, I can hear you!
    J-->>-A: I feel great!

    Note right of A: Text in note
    Note left of A: Text in note
    Note RIGHT of J: Text in note
    Note left of J: Text in note
    Note over A,J: A typical interaction

    loop Every minute
        Note right of J: 循环里边继续提示
        Note right of A: 提示
        Note over A,J: 循环里边提示
        A --> J: Great!
        A -> A : 自己循环
    end

     A->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>A: Not so good :(
    else is well
        Bob->>A: Feeling fresh like a daisy
    end
    opt Extra response
        Bob->>A: Thanks for asking
    end
```


##### 甘特图
```mermaid
gantt
       dateFormat  YYYY-MM-DD
       title Adding GANTT diagram functionality to mermaid

       section A section
       Completed task            :done,    des1, 2014-01-06,2014-01-08
       Active task               :active,  des2, 2014-01-09, 3d
       Future task               :         des3, after des2, 5d
       Future task2              :         des4, after des3, 5d

       section Critical tasks
       Completed task in the critical line :crit, done, 2014-01-06,24h
       Implement parser and jison          :crit, done, after des1, 2d
       Create tests for parser             :crit, active, 3d
       Future task in critical line        :crit, 5d
       Create tests for renderer           :2d
       Add to mermaid                      :1d

       section Documentation
       Describe gantt syntax               :active, a1, after des1, 3d
       Add gantt diagram to demo page      :after a1  , 20h
       Add another diagram to demo page    :doc1, after a1  , 48h

       section Last section
       Describe gantt syntax               :after doc1, 3d
       Add gantt diagram to demo page      :20h
       Add another diagram to demo page    :48h
```