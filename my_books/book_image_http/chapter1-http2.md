### 6. HTTP首部
**HTTP报文大致分为 报文首部 和 报文主体**

1. HTTP报文首部
*HTTP 协议的请求和响应报文中必定包含 HTTP 首部。首部内容为客
户端和服务器分别处理请求和响应提供所需要的信息。*

* 请求报文：由方法、URI、HTTP版本、HTTP首部字段 等部分构成 （参考 3.2报文结构）
* 响应报文：由HTTP版本、状态码（数字和原因短语）、HTTP首部字段3部分构成

2. HTTP首部字段
    ```
    HTTP 首部字段是构成 HTTP 报文的要素之一。
    在客户端与服务器之间以 HTTP 协议进行通信的过程中,无论是请求还是响应都会使用首部字段,它能起到传递额外重要信息的作用。
    使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等内容。
    ```
    *结构*： 首部字段名：字段值

3. 4种HTTP首部字段类型
    ```
    通用首部字段：请求报文和响应报文两方都会使用的首部

    请求首部字段：从客户端向服务器端发送请求报文时使用的首部。补充了请求的附加内容、客户端信息、响应内容相关优先级等信息。

    响应首部字段：从服务器端向客户端返回响应报文时使用的首部。补充了响应的附加内容,也会要求客户端附加额外的内容信息

    实体首部字段：针对请求报文和响应报文的实体部分使用的首部。补充了资源内容更新时间等与实体有关的信息。

4. HTTP/1.1通用首部字段
    ```
    Cache-Control：
    Connection：
        控制不再转发给代理的首部字段
        管理持久连接
    Date:
        首部字段 Date 表明创建 HTTP 报文的日期和时间。
    Trailer:
        首部字段 Trailer 会事先说明在报文主体后记录了哪些首部字段。该首部字段可应用在 HTTP/1.1 版本分块传输编码时
    Transfer-Encoding:
        规定了传输报文主体时采用的编码方式
    Upgrade:
    Via:
    Warning:
    ```
5. 请求首部字段
    ```
    请求首部字段是从客户端往服务器端发送请求报文中所使用的字段,用于补充请求的附加信息、客户端信息、对响应内容相关的优先级等内容。
    ```
    1. Accept
    (Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.)
    Accept 首部字段可通知服务器,用户代理能够处理的媒体类型及媒体类型的相对优先级。可使用 type/subtype 这种形式,一次指定多种媒体类型。
    ```
        文本文件
        text/html, text/plain, text/css ...
        application/xhtml+xml, application/xml ...

        图片文件
        image/jpeg, image/gif, image/png ...

        视频文件
        video/mpeg, video/quicktime ...

        应用程序使用的二进制文件
        application/octet-stream, application/zip ...
    ```
    2. Accept-Charset
    (Accept-Charset: iso-8859-5, unicode-1-1;q=0.8)
    Accept-Charset 首部字段可用来通知服务器用户代理支持的字符集及字符集的相对优先顺序。另外,可一次性指定多种字符集。该首部字段应用于内容协商机制的服务器驱动协商。
    *与首部字段 Accept 相同的是可用权重 q 值来表示相对优先级。*

    3. Accept-Encoding
    (Accept-Encoding: gzip, deflate)
    Accept-Encoding 首部字段用来告知服务器用户代理支持的内容编码及内容编码的优先级顺序。可一次性指定多种内容编码

    4. Accept-Language
    (Accept-Language: zh-cn,zh;q=0.7,en-us,en;q=0.3)

    5. Authorization

    6. Expect

    7. From

    8. Host
    首部字段 Host 会告知服务器,请求的资源所处的互联网主机名和端口号。
    **Host 首部字段在 HTTP/1.1 规范内是唯一一个必须被包含在请求内的首部字段。**

    9. If-Match
    形如 If-xxx 这种样式的请求首部字段,都可称为条件请求。服务器接
收到附带条件的请求后,只有判断指定条件为真时,才会执行请求。

    10. If-Modified-Since
    If-Modified-Since 用于确认代理或客户端拥有的本地资源的有效性。获取资源的更新日期时间,可通过确认首部字段 Last-Modified 来确定。如果资源在这个时间之后更新过，服务器接受请求。如果在这个时间之后么有更新过，返回304 Not Modified

    11. If-None-Match
    12. If-Range
    13. If-Unmodified-Since
    14. Max-Forwards
    15. Proxy-Authorization
    16. Range
    17. Referer
    首部字段 Referer 会告知服务器请求的原始资源的 URI。
    18. TE
    19. User-Agent
    User-Agent 用于传达浏览器的种类
    首部字段 User-Agent 会将创建请求的浏览器和用户代理名称等信息传达给服务器。
    由网络爬虫发起请求时,有可能会在字段内添加爬虫作者的电子邮件地址。
    此外,如果请求经过代理,那么中间也很可能被添加上代理服务器的名称。

6. 响应首部字段
    响应首部字段是由服务器端向客户端返回响应报文中所使用的字段,用于补充响应的附加信息、服务器信息,以及对客户端的附加要求等信息。

    1. Accept-Ranges
    （Accept-Ranges: bytes）
    2. Age
    首部字段 Age 能告知客户端,源服务器在多久前创建了响应。字段值的单位为秒。
    3. ETag
    4. Location
    使用首部字段 Location 可以将响应接收方引导至某个与请求 URI 位置不同的资源。
    基本上,该字段会配合 3xx :Redirection 的响应,提供重定向的URI。
    5. Proxy-Authenticate
    6. Retry-After
    7. Server
    首部字段 Server 告知客户端当前服务器上安装的 HTTP 服务器应用程序的信息。
    8. Vary
    9. WWW-Authenticate

7. 实体首部字段
    实体首部字段是包含在请求报文和响应报文中的实体部分所使用的首部,用于补充内容的更新时间等与实体相关的信息。
    1. Allow
    （Allow: GET, HEAD
    首部字段 Allow 用于通知客户端能够支持 Request-URI 指定资源的所有 HTTP 方法。当服务器接收到不支持的 HTTP 方法时,会以状态码405 Method Not Allowed 作为响应返回。与此同时,还会把所有能支持的 HTTP 方法写入首部字段 Allow 后返回。
    2. Content-Encoding
    首部字段 Content-Encoding 会告知客户端服务器对实体的主体部分选用的内容编码方式
    3. Content-Language
    首部字段 Content-Language 会告知客户端,实体主体使用的自然语言(指中文或英文等语言)。
    4. Content-Length
    表明了实体主体部分的大小(单位是字节)
    5. Content-Location
    给出与报文主体部分相对应的 URI。和首部字段 Location 不同,Content-Location 表示的是报文主体返回资源对应的 URI。
    6. Content-Type
    (Content-Type: text/html; charset=UTF-8)
    首部字段 Content-Type 说明了实体主体内对象的媒体类型。和首部字段 Accept 一样,字段值用 type/subtype 形式赋值。
    参数 charset 使用 iso-8859-1 或 euc-jp 等字符集进行赋值
    7. Expires
    8. Last-Modified

8. 为Cookie服务的首部字段
    ```
    首部字段名    说明                        首部类型
    Set-Cookie  开始状态管理所使用的Cookie信息  响应首部字段
    Cookie      服务器接收到的Cookie信息       请求首部字段
    ```

    Set-Cookie：
    （Set-Cookie: status=enable; expires=Tue, 05 Jul 2011 07:26:31 GMT）

### 7. HTTPS
通过和 SSL(Secure Socket Layer,安全套接层)或 TLS(Transport Layer Security,安全层传输协议)的组合使用, 加密 HTTP 的通信内容。

1. HTTP的缺点
    ```
    1. 通信使用明文(不加密),内容可能会被窃听
    2. 不验证通信方的身份,因此有可能遭遇伪装
    3. 无法证明报文的完整性,所以有可能已遭篡改
    ```
2. HTTP+ 加密 + 认证 + 完整性保护=HTTPS

### 8.确认访问用户身份的认证

1. BASIC认证
    认证不够灵活，安全等级不够
2. DIGEST认证
    仍不灵活，安全仍不够。
3. SSL客户端认证
    费用等问题
4. 基于表单认证
    现在常用的认证方式，结合cookie使用管理session

### 9. 基于HTTP的功能追加协议
略
### 10. 构建Web内容的技术
1. HTML
2. 动态HTML
3. Web应用
### 11. Web的攻击技术
略
