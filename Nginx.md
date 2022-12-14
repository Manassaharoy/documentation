# NGINX Introduction and setup

NGINX setup

```
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl stop nginx
```

Nginx default.conf file :

```
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	server_name _;

location /apipoint/ {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_pass http://nodeserver:8082/;
    }
location / {

        root /var/www/html;

		try_files $uri /index.html;
    }

	# pass PHP scripts to FastCGI server
	#
	#location ~ \.php$ {
	#	include snippets/fastcgi-php.conf;
	#
	#	# With php-fpm (or other unix sockets):
	#	fastcgi_pass unix:/run/php/php7.4-fpm.sock;
	#	# With php-cgi (or other tcp sockets):
	#	fastcgi_pass 127.0.0.1:9000;
	#}

	# deny access to .htaccess files, if Apache's document root
	# concurs with nginx's one
	#
	#location ~ /\.ht {
	#	deny all;
	#}
}

server {
	 listen 443 ssl ;
	 listen [::]:443 ssl ;
     ssl_certificate /etc/nginx/conf.d/fullchain.pem; # managed by Certbot
     ssl_certificate_key /etc/nginx/conf.d/privkey.pem; # managed by Certbot

    server_name domain.com www.domain.com; # managed by Certbot

location /apipoint/ {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_pass http://nodeserver:8082/;
    }
    location / {
        # root /usr/share/nginx/html;
        root /var/www/html;
        # try_files $uri?$args $uri/ $uri.html?$args /server.js?$args;
		try_files $uri /index.html;
    }

	# pass PHP scripts to FastCGI server
	#
	#location ~ \.php$ {
	#	include snippets/fastcgi-php.conf;
	#
	#	# With php-fpm (or other unix sockets):
	#	fastcgi_pass unix:/run/php/php7.4-fpm.sock;
	#	# With php-cgi (or other tcp sockets):
	#	fastcgi_pass 127.0.0.1:9000;
	#}

	# deny access to .htaccess files, if Apache's document root
	# concurs with nginx's one
	#
	#location ~ /\.ht {
	#	deny all;
	#}

}
server {
    if ($host = www.domain.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    if ($host = domain.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

	listen 80 ;
	listen [::]:80 ;
    server_name domain.com www.domain.com;
    return 404; # managed by Certbot
}
```

error.log
```
tail -f /var/log/nginx/error.log
```
