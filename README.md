title: nginx
speaker: 胡建霞
url: https://github.com/ksky521/nodePPT
transition: cards
files: /js/demo.js,/css/demo.css
 
[slide]
 
# nginx 基础配置
## 演讲者：胡建霞
 
[slide]
 
# 基础配置讲解 {:&.flexbox.vleft}
### nginx 基本结构 nginx.conf文件
```javascript
worker_processes 1;#全局生效
events {
    worker_connections 1024;#在events中生效
}
http { #以下指令只能在http中生效
    include mime.types;
    default_type application/octet-stream;
    sendfile on;
    keepalive_timeout 65;
    server { #server块
        listen 80;
        server_name localhost;
        location /{ #location块
            root html;
            index index.html index.htm;
        }
    }
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root html;
    }
}
```
讲解一下root
 
[slide]
 
# 全局块 events块 http块 {:&.flexbox.vleft}
### **全局块:**从头部开始到events之间的内容，配置影响nginx服务器整体运行的指令
----
 
#### eg：worker_processes number | auto；
----
 
### **events块:**涉及到的指令主要影响nginx服务器与用户的网络连接
----
 
### **http块:** 配置代理 缓存和日志定义等绝大多数的功能和第三方模块的配置
 
[slide]
## 基于ip配置nginx访问权限
 
 
```javascript
location / {
    deny 192.168.1.103;#禁止ip
    allow 192.168.1.1;#允许ip
    deny all;
}
```
## 日志配置
----
 
```javascript
    error_log file | stderr [debug | info | notice | warn | error | crit | alert | emerg];
    error_log  /var/log/nginx/error.log;
```
 
```javascript
    log_format custom '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $request_time $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" "$request_body"';
    access_log /var/log/nginx/access.log custom;
```
##更改location 的 URI
```javascript
    location ~ ^/data/(.+\.(html|htm))$ {
        alias /locationtest1/other/;
    }
```
 
[slide]
### nginx服务器的Gzip
```javascript
    gzip  on;#开启gzip功能
    gzip_min_length  5k;#响应页数据上限
    gzip_buffers     4 16k;#缓存空间大小
    gzip_http_version 1.0;#检查http协议版本在这之上才开启gzip
    gzip_comp_level 4;#压缩等级 1-9
    gzip_types       text/plain application/x-javascript text/css application/xml application/json text/javascript application/x-httpd-php image/jpeg image/gif image/png;#压缩文件类型
    gzip_vary on;#启用压缩标志 会带上accept-encoding gzip
    gunzip_static on| off;默认关闭 是检测客户端浏览器是否支持gzip处理 检查预压缩文件
    gzip_disable "MSIE [1-6]\.(?!.*SV1)";#检测是 msie4 5就不开启gzip
```
 
### nginx服务器的rewrite功能
 
 
[slide]
 
# nginx缓存的使用
 
[note]
##这里是note
 
使用n键，才能显示
[/note]
## nginx缓存
### note笔记是多窗口，或者自己做一些笔记用的
---
按下键盘【N】键测试下note，
 
markdown语法如下：
```markdown
这里是　note的外表标题
```
 
[slide]
## 一篇nginx基础文
----
<iframe data-src="http://www.cnblogs.com/zerohu/p/6202562.html" src="about:blank;"></iframe>

[slide]
# 补充说明一下:以上文档可以使用nodeppt播放
