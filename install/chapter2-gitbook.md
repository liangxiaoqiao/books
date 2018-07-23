### win 安装过程
1. 安装python3
2. 安装nodejs
3. npm install gitbook-cli -g



### Deepin安装过程

1. 安装python3

2. 安装nodejs

   1. 官网下载node-linux.tar

   2. 解压并移动到文件夹 /opt/node

   3. 建立全局变量 

      sudo ln -s /opt/node/bin/node /usr/local/bin/node   

      sudo ln -s /opt/node/bin/npm /usr/local/bin/npm

   4. node -v    npm -v查看安装成功

   5. 可选：安装cnpm   `npm install -g cnpm --registry=https://registry.npm.taobao.org`
     `sudo ln -s /opt/node-v8.11.3-linux-x64/bin/cnpm /usr/local/bin`


3. npm install gitbook-cli -g    (安装gitbook)
4. sudo ln -s /opt/node-v8.11.3-linux-x64/bin/gitbook  /usr/local/bin   （建立软连接）

