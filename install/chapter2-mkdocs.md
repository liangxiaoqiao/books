### mkdocs ubuntu安装步骤
1. 安装python3
    ```text
    建议安装python3。教程网上很多，搜下就行了。
    切换python2 到 python3
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150

    如果要切换到Python2，执行：
    sudo update-alternatives --config python
    ```
1. 确认python3安装成功:
    ```
    python --version
    ```

1. 安装pip3:
    ```shell
    sudo apt-get isntall python3-pip
    ```

1. 确认pip3安装成功：
    ```
    pip3 --version
    ```
1. 安装MkDocs：
    ```
    pip3 install mkdocs
    ```
1. 确认MkDocs安装成功：
    ```
    mkdocs --version
    ```




#### MkDocs主题
[MkDocs第三方主题网址](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)
