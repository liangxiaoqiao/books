## Ubuntu命令
1. ssh远程登录： ssh ubuntu@110.230.210.36
1. ssh添加文件： ssh-add ~/.ssh/id_rsa

1. 更换源
    ```bash
    sudo gedit /etc/apt/sources.list
    ```
1. 启动jekins
    ```shell
    jenkins  sudo service jenkins start
    jenkins colter liangchao123
    ```
1. apt-get不能进行
    ```
    Could not get lock /var/lib/apt/lists/lock
    ps -ef | grep apt-get   查看进程
    ```
1. alias ll 查看别名
    ```shell
    alias设置只对当前起作用，想要一直起效，修改~/.bashrc目录 增加自己的alias
    例如  alias lf='ls -lF'
    ```
1. nautilus 打开文件夹


## Deepin
1. 安装JDK

2. 安装maven
    1. 官网下载apache-maven-3.5.3-bin.tar.gz
    1. 移动到/usr/lib
    1. 解压  sudo tar -zxvf apache-maven-3.5.3-bin.tar.gz
    1. 添加环境变量 sudo vim /etc/profile
    1. 追加 



