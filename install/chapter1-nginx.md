### nginx 安装

##### linux安装

1. sudo apt-get install nginx

   ```
   安装好的文件位置：
   /usr/sbin/nginx：主程序
   /etc/nginx：存放配置文件
   /usr/share/nginx：存放静态文件
   /var/log/nginx：存放日志
   ```

2. 配置软连接  sudo ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx

3. 启动 nginx ： sudo nginx   关闭： sudo nginx -s quit

4. 配置根据域名转发

   ```
   进入 /etc/nginx/conf.d  创建 default.conf
   配置文件:
   server {
     listen 80;
       server_name www.liangxiaoqiao.com;
       location / {
           proxy_pass http://127.0.0.1:4000;
       }
   }

   server {
     listen 80;
       server_name doc.liangxiaoqiao.com;
       location / {
           proxy_pass http://127.0.0.1:8000;
       }
   }

   server {
     listen 80;
       server_name liangxiaoqiao.com;
       location / {
           proxy_pass http://127.0.0.1:4000;
       }
   }

   重启
   ```




##### Windows安装

1. Windowns下安装
    * 进入官网，下载windows下压缩包
    * 解压，打开cmd，进入解压文件夹
    * cmd执行 start nginx启动

```
判断是否启动：
解压目录执行 nginx -V
直接进程中查找ngnix。
打开 http://127.0.0.1
```
