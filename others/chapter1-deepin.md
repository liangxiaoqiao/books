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
    1. 查看是否安装成功： mvn --version

3. 安装gradle
    1. 官网下载gradle-4.7.zip
    1. 移动到/usr/lib
    1. 解压  sudo unzip gradle-4.7.zip
    1. 添加环境变量 sudo vim /etc/profile
    1. 文件最后加上环境变量：

        ```bash 
        export GRADLE_HOME=/usr/lib/gradle-4.7
        export PATH=$GRADLE_HOME/bin:$PATH
        ```

    1. 查看是否安装成功： gradle --version

## ArchLinux 
1. manjaro基于archlinux
1. 汉语输入法不成功：[官网wiki](https://wiki.archlinux.org/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

    ```shell
    sudo pacman -S fcitx fcitx-im

    安装fcitx后不能切换到中文输入法，搜索arch wiki,查看：arch fcitx 配置 打开 ~/.xprofile文件，添加以下代码：

    #fcitx
    export GTK_IM_MODULE=fcitx 
    export QT_IM_MODULE=fcitx 
    export XMODIFIERS="@im=fcitx"



    如果 Fcitx 没有随桌面环境自动启动，或者您想修改下 Fcitx 启动参数，请用桌面环境提供的自动启动工具配置，或者直接编辑用户目录~/.config/autostart/ 下的 fcitx-autostart.desktop 文件以确认自动启动是否被禁用。如果用户目录下的文件并不存在，您可以复制自动启动文件 /etc/xdg/autostart/fcitx-autostart.desktop 到用户目录：

    cp /etc/xdg/autostart/fcitx-autostart.desktop  ~/.config/autostart/
    ```


## Ubuntu命令
1. Linux Mint  Lubuntu Xubuntu都是基于ubuntu。
1. ssh远程登录： ssh ubuntu@110.230.210.36
1. ssh添加文件： ssh-add ~/.ssh/id_rsa

1. alias ll 查看别名

    ```shell
    alias设置只对当前起作用，想要一直起效，修改~/.bashrc目录 增加自己的alias
    例如  alias lf='ls -lF'
    ```

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
 
    ```bash
    adfasdfasdf
    could not get lock /var/lib/apt/lists/lock
    ps -ef | grep apt-get   查看进程
    ```

1. nautilus 打开文件夹
