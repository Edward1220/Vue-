# vue 项目部署方式和解决跨域问题反向代理配置

## 1. Nginx 方式托管和反向代理配置

### 	1.1	下载 对应的Nginx 版本 

> https://nginx.org/en/download.html

### 	1.2 	解压Nginx压缩包

<img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524091019519.png" alt="image-20210524091019519"  />

### 	1.3 	托管项目文件配置

> nginx 目录下的conf文件夹——>nginx.cof 文件
>
> 配置Vue 项目打包后的dist文件夹路径

​	<img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524091601877.png" alt="image-20210524091601877"  />

### 1.4	 反向代理配置

> 新增 location /api 节点，配置 api 访问路径

​		<img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524091746955.png" alt="image-20210524091746955"  />

### 1.5	格式参考

```bash
    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   D:\SourceCode\iie-erp-assist\src\client\iie-erp-assist-client\dist;
            index  index.html index.htm;
        }

        location /api {
            proxy_pass  http://192.168.0.62:8070/api;
        }
        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
```



### 1.6	nginx 相关命令

```
在nginx.exe目录，打开命令行工具，用命令 启动/关闭/重启nginx  

start nginx ：启动nginx

nginx -s reload ：修改配置后重新加载生效

nginx -s reopen ：重新打开日志文件

nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

nginx -s stop :快速停止nginx

nginx -s quit ：完整有序的停止nginx
```



## 2.	IIS 方式托管和反向代理配置

### 	2.1	安装ARR(Application Request Route) 为 IIS 开启代理

> 安装后重启 IIS 会显示 Application Request Route Cache，打开该功能开启代理功能

### <img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095019334.png" alt="image-20210524095019334"  />

<img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095140945.png" alt="image-20210524095140945"  />

<img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095209453.png" alt="image-20210524095209453"  />

### 	2.2	安装urlrewrite 配置url重写

> 选中一个项目，配置 RUL 重写 

![image-20210524095701291](C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095701291.png)

> 添加规则

![image-20210524095834819](C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095834819.png)

> 配置规则

## <img src="C:\Users\xp\AppData\Roaming\Typora\typora-user-images\image-20210524095332393.png" alt="image-20210524095332393"  />

