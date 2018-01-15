### Spring整体架构
1. spring-core:主要包含Spring框架基本的核心工具类。Spring的其他组件都要使用到这个包里的类，core模块是其他组件的基本核心。
2. spring-beans：所有应用都要用到的，包含访问配置文件，创建和管理bean，以及进行IOC/DI 操作相关的类。
3. spring-context：构建于Core和Beans智商，提供了一种类似于JNDI注册器的框架式对象访问方法。Context模块继成了Beans的特性，为Spring核心提供了大量扩展，添加了对国际化、事件传播，资源加载和对Context的透明创建的支持。
4. web模块
5. aop模块
