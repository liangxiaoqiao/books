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
    1. 下载JDK对应版本linux64包
    2. sudo mv jdk8.tar.gz /usr/lib/jvm
    3. sudo tar -zxvf jdk8.tar.gz
    4. sudo vi /etc/profile
    5. 文件最后加上环境变量：

        ```bash
        export JAVA_HOME=/usr/lib/jvm/jdk8
        export JRE_HOME=${JAVA_HOME}/jre
        export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
        export PATH=${JAVA_HOME}/bin:$PATH
        ```

    6. 查看当前java优先级：*sudo update-alternatives --config java*  看到默认的优先级是1081
    7. 设置优先级比1081大

        ```bash
            sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk8/bin/java 3000 
            sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk8/bin/javac 3000 
            sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk8/bin/jar 3000
        ```

    8. 查看是否安装成功： java --version 

2. 安装maven
    1. 官网下载apache-maven-3.5.3-bin.tar.gz
    1. 移动到/usr/lib
    1. 解压  sudo tar -zxvf apache-maven-3.5.3-bin.tar.gz
    1. 添加环境变量 sudo vim /etc/profile
    1. 文件最后加上环境变量：

        ```bash 
        export M2_HOME=/usr/lib/apache-maven-3.5.3
        export PATH=$M2_HOME/bin:$PATH
        ```



