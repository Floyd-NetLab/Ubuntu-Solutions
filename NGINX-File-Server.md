# How to Setup Nginx Fileserver For File Sharing

## First login to your server via ssh or telnet

```
mkdir fileserver
```

```
cd fileserver
```

```
nano default.config
```

## copy paste this section

```
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        autoindex on;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
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

```
nano docker-compose.yml
```

## copy paste this section

```
version: '3'
services:
  nginx:
    image: nginx:stable-alpine-slim
    volumes:
      - ./default.conf:/etc/nginx/conf.d/default.conf:ro
      - ./data/:/usr/share/nginx/html:ro 
    ports:
      - 80:80
```
```
mkdir data
```

```
docker-compose pull
```

```
docker-compose up -d
```





#### you can upoload ,download ,create folder ,delete folder files using filezilla 
