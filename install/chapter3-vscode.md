##### VS Code设置Markdown支持流程图、时序图等

1. VSCode选择左侧 Extensions面板，搜索Markdown Preivew Enhanced，安装

2. 插件以及markdown的一些语法，参考[插件文档](<https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/>)

3. Ctrl+Shift+P 搜索settings，选择Preferences:Open Settings(JSON)，打开设置文件

4. 添加json字段，修复 mermaid图是黑框的问题

   ```json
   "markdown-preview-enhanced.mermaidTheme": "forest"
   ```

   

5. ~~plantuml不能执行问题~~ 
    ~~"plantuml.commandArgs": [
       "-DGRAPHVIZ_DOT=\"D:/Users/Nonghorn/Personal App/graphviz/bin/dot.exe\"",
   ]~~

6. plantuml不能执行问题

   ```
   安装 graphviz（参看下边的下载地址）
   添加环境变量 （路径为你的安装路径）
   DGRAPHVIZ_DOT  D:/Users/Nonghorn/Personal App/graphviz/bin/dot.exe
   ```

   

7. [Graphviz下载地址](<https://graphviz.gitlab.io/_pages/Download/Download_windows.html>)

8. 导出PDF，需要安装 princexml ，将C:\Program Files (x86)\Prince\engine\bin加入path环境变量

9. [prince下载地址](<https://www.princexml.com/download/>)

10. 导出PDF，有两种方式 一种是上边的，另外一种是使用chrome的预览功能。（prince导出时，有图片会需要下载其他东西，导出后有标题书签。chrome导出后图片正常，没有标题书签）



##### Demo

```mermaid
graph LR;
id  
id1[text in the box]
id2(text in round box)
id3((text int the circle))

A-->B;
A-->C;
B-->D;
C-->D;
C-->id1;
id1--> id3;
```


```mermaid 
sequenceDiagram
    participant Alice
    participant Bob
    Alice -> John: Hello John, how are you?
    loop Healthcheck
        John->John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/> prevail...
    John-->Alice: Great!
    John->Bob: How about you?
    Bob-->John: Jolly good!
```

```mermaid
sequenceDiagram
A->> B: Query
B->> C: Forward query
Note right of C: Thinking...
C->> B: Response
B->> A: Forward response
```
```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
```
```mermaid
gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid
        section A section
        Completed task            :done,    des1, 2014-01-06,2014-01-08
        Active task               :active,  des2, 2014-01-09, 3d
        Future task               :         des3, after des2, 5d
        Future task2               :         des4, after des3, 5d
        section Critical tasks
        Completed task in the critical line :crit, done, 2014-01-06,24h
        Implement parser and jison          :crit, done, after des1, 2d
        Create tests for parser             :crit, active, 3d
        Future task in critical line        :crit, 5d
        Create tests for renderer           :2d
        Add to mermaid                      :1d

```

```puml
@startuml
    participant Alice
    participant Bob
    Alice->John: Hello John, how are you?
    loop Healthcheck
        John->John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/> prevail...
    John-->Alice: Great!
    John->Bob: How about you?
    Bob-->John: Jolly good!
@enduml
```
```sequence {{theme="hand"}}
A->>B: How are you?
B->>A: Great!
```

```puml
@startuml
A ->> B : How are you?
B ->> A : Great!
@enduml
```


```puml
@startuml

title 时序图

== 鉴权阶段 ==

Alice -> Bob: 请求
Bob -> Alice: 应答

== 数据上传 ==

Alice -> Bob: 上传数据
note left: 这是显示在左边的备注

Bob --> Canny: 转交数据
... 不超过 5 秒钟 ...
Canny --> Bob: 状态返回
note right: 这是显示在右边的备注

Bob -> Alice: 状态返回

== 状态显示 ==

Alice -> Alice: 给自己发消息
@enduml
```

```puml
@startuml
!include <cloudinsight/tomcat>
!include <cloudinsight/kafka>
!include <cloudinsight/java>
!include <cloudinsight/cassandra>
title Cloudinsight sprites example
skinparam monochrome true
rectangle "<$tomcat>\nwebapp" as webapp
queue "<$kafka>" as kafka
rectangle "<$java>\ndaemon" as daemon
database "<$cassandra>" as cassandra
webapp -> kafka
kafka -> daemon
daemon --> cassandra
@enduml
```

```puml
@startuml
Object <|-- ArrayList

Object : equals()
ArrayList : Object[] elementData
ArrayList : size()

@enduml
```