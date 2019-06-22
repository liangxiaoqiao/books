##### VS Code设置Markdown支持流程图、时序图等

1. VSCode选择左侧 Extensions面板，搜索Markdown Preivew Enhanced，安装

2. 插件以及markdown的一些语法，参考[插件文档](<https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/>)

3. Ctrl+Shift+P 搜索settings，选择Preferences:Open Settings(JSON)，打开设置文件

4. 添加json字段，修复 mermaid图是黑框的问题

   ```json
   "markdown-preview-enhanced.mermaidTheme": "forest
   ```

   

5. ~~plantuml不能执行问题~~ 

   ```json
   "plantuml.commandArgs": [
       "-DGRAPHVIZ_DOT=\"D:/Users/Nonghorn/Personal App/graphviz/bin/dot.exe\"",
   ]
   ```

6. plantuml不能执行问题

   ```
   添加环境变量
   DGRAPHVIZ_DOT  D:/Users/Nonghorn/Personal App/graphviz/bin/dot.exe
   ```

   

7. [Graphviz下载地址](<https://graphviz.gitlab.io/_pages/Download/Download_windows.html>)

8. 导出PDF，需要安装 princexml ，将C:\Program Files (x86)\Prince\engine\bin加入path环境变量

9. [prince下载地址](<https://www.princexml.com/download/>)

10. 导出PDF，有两种方式 一种是上边的，另外一种是使用chrome的预览功能。（prince导出时，有图片会需要下载其他东西，导出后有标题书签。chrome导出后图片正常，没有标题书签）



##### Demo

```mermaid
graph TD;
A-->B;
A-->C;
B-->D;
C-->D;
```


```mermaid 
sequenceDiagram
    participant Alice
    participant Bob
    Alice->John: Hello John, how are you?
    loop Healthcheck
        John->John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail...
    John-->Alice: Great!
    John->Bob: How about you?
    Bob-->John: Jolly good!
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


```sequence {{theme="hand"}}
A->>B: How are you?
B->>A: Great!
```

```puml
@startuml
testdot
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