- websocket error
Config dưới đây fix được vấn đề trên
```
server {
  listen 80;
  server_name nb.lamkhatinh.com;
  server_tokens off;
  location /.well-known/acme-challenge/ {
    root /var/www/certbot;
  }
  location / {
    return 301 https://$host$request_uri;
  }
}
server {
  listen 443 ssl;
  server_name nb.lamkhatinh.com;
  server_tokens off;
  ssl_certificate /etc/letsencrypt/live/nb.lamkhatinh.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/nb.lamkhatinh.com/privkey.pem;
  include /etc/letsencrypt/options-ssl-nginx.conf;
  ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
  location / {
   proxy_pass      http://192.168.1.40:8888;
   proxy_http_version 1.1;
   proxy_set_header Upgrade $http_upgrade;
   proxy_set_header Connection "upgrade";
   proxy_set_header Origin "";
  }
}
```
Phần có tác dụng fix lỗi
```
   proxy_http_version 1.1;
   proxy_set_header Upgrade $http_upgrade;
   proxy_set_header Connection "upgrade";
   proxy_set_header Origin "";
```