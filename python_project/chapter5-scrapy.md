1. #### 过程

   1. 创建项目

   ```bash
   	scrapy startproject leetcode_spider
   ```

   1. 定义提取的Item
   2. 编写爬去网站的spider并提取item
   3. 编写Item Pipeline来存储提取到的Item（即数据）

1. #### 结构 

```text
tutorial/
    scrapy.cfg
    tutorial/
        __init__.py
        items.py
        pipelines.py
        settings.py
        spiders/
            __init__.py
            ...
这些文件分别是:

scrapy.cfg: 项目的配置文件
tutorial/: 该项目的python模块。之后您将在此加入代码。
tutorial/items.py: 项目中的item文件.
tutorial/pipelines.py: 项目中的pipelines文件.
tutorial/settings.py: 项目的设置文件.
tutorial/spiders/: 放置spider代码的目录.
```

