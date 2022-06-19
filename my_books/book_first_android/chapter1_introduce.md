
#### Android系统架构
1. Linux内核层：底层驱动（如 显示 音频 照相机 蓝牙 wifi等）
2. 系统运行层： 数据库，3D绘图，webkit提供浏览器内核支持
3. 应用框架层： 构建应用程序可能用到的各种API
4. 应用层： 所有手机上的APP

#### 系统提供
1. 四大组件： 活动（Activity） 服务（Service）广播接收器（Broadcast Receiver）内容提供器（Content Provider）
2. 丰富的系统控件
3. SQLite数据库
4. 多媒体
5. 定位

#### 其他
1. 引用资源： 代码中：R.string.app_name   XML文件中：@string/app_name
2. 日志： Log.v d i w e对应不用级别的日志 （Logca Filter过滤）
