1. MySQL连接乱码
    ```
     String url = "jdbc:mysql://localhost:3306/act_test3?useUnicode=true&characterEncoding=UTF-8";  
    ```
    
1. Tomcat启用SHTML
    ```
    http://tomcat.apache.org/tomcat-7.0-doc/ssi-howto.html
    web.xml启用SSI Servelt  SSI Filter（不要忘记匹配路径。有的时候可能需要匹配 *.shtml  和 *.html）
    context.xml  Context加上属性  privileged="true"
    
    SHTML乱码问题：加入属性
    		<init-param>
    			<param-name>inputEncoding</param-name>
    			<param-value>utf-8</param-value>
    		</init-param>
    		<init-param>
    			<param-name>outputEncoding</param-name>
    			<param-value>utf-8</param-value>
    		</init-param>
    
    Tomcat修改路径   
    server.xml找到<Host>节点
    <Context path=""  docBase="manual"   ></Context>   docBase是文件夹    path是访问路径
    ```
1. 多次读取同一个InputStream
    ```java
    // 多次读取同一个InputStream会出现NullPoint将InputStream转换成ByteArray，然后读取  
     InputStream in = new FileInputStream("C:\\Users\\user\\Desktop\\image\\1415884219203.jpg");


        ByteArrayOutputStream baos = new ByteArrayOutputStream();  
        byte[] buffer = new byte[1024];  
        int len;  
        while ((len = in.read(buffer)) > -1 ) {  
            baos.write(buffer, 0, len);  
        }  
        baos.flush();                


        BufferedImage image1 = ImageIO.read(new ByteArrayInputStream(baos.toByteArray()));

        System.out.println(image1.getWidth());

        BufferedImage image2 = ImageIO.read(new ByteArrayInputStream(baos.toByteArray()));

        System.out.println(image2.getWidth());
    ```