---
layout: post
title: WordPress 建站
category: 技术
# date: 2017-11-28 00:05:47
tags: WordPress
keywords: WordPress
published: true
---

# WordPress 建站

<iframe scrolling="no" frameborder="0" allowtransparency="true" src="https://platform.twitter.com/widgets/widget_iframe.704fca4914c9b90d7a9d41abcaa19933.html?origin=https%3A%2F%2Fcolorsnapper.com&amp;settingsEndpoint=https%3A%2F%2Fsyndication.twitter.com%2Fsettings" title="Twitter settings iframe" style="display: none;"></iframe>

使用 docker-compose.yml 搭建。

## 问题

1.表单里面的所有文件上传，需要修改大小的限制(最大允许 100MB )，需要修改 nginx & wordpress 的配置

在 nginx 字段中修改：

```
# nginx 代码修改:
# 所在路径
$ cd /etc/nginx/sites-enabled/member
$ vim zbqy.conf
server {
        listen  80;
        server_name zbqy.updis.haomo-tech.com;
        # 修改上传文件大小为 100M
        client_max_body_size   100m;

             location /    {
                    proxy_pass    http://127.0.0.1:6164;
                    proxy_set_header    Host            $host;
                    proxy_set_header    X-Real-IP       $remote_addr;
                    proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                }
}
```

docker 修改(文件大小上传 2M 限制问题):

```
# 登录服务器查询 wordpress 所在的 docker 容器 id
$ docker ps -a
# 进入容器 bash
$ docker exec -it 668d2409bf87 bash
```

在 docker-library/wordpress 镜像中，目前没有默认的 php.ini 文件，解决的方法有两种，推荐的为第二种：

a.）在 docker file 里添加下面两行：<br /><br />

```
RUN touch /usr/local/etc/php/conf.d/uploads.ini \ && echo "upload_max_filesize = 10M;" >> /usr/local/etc/php/conf.d/uploads.ini
# 但是 docker registry 推荐在 /usr/local/lib 目录下增加一个自定义的 php.ini 文件 。
```

b.）修改   .htaccess 文件：

进入 docker，在根目录运行如下命令查找到该文件。

```
$ find . -name '.htaccess'
# 我的文件地址在：/var/www/html/.htaccess
$ vi .htaccess

# 修改如下(按照需求改成 100M)：
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]

# add by yh, modify upload file size.
php_value post_max_size 100M
php_value upload_max_filesize 100M

```

## WordPress 参考

- https://github.com/miziomon/awesome-wordpress
- 