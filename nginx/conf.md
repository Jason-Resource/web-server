## nginx支持php访问
test.conf
```
server {
    listen 80;
    server_name test.cc;
    root /home/wwwroot/test;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
        #try_files $uri /index.php =404;
        #fastcgi_split_path_info ^(.+\.php)(/.+)$;
    }
}
```
