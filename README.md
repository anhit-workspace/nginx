# Nginx và một số vấn đề thường gặp (Issue)

# I. Nginx: Install

### Step 1: Update apt and install nginx

```
sudo apt update
sudo apt install nginx
```

### Step 2: Config Firewall

Firewall Ubuntu

```
sudo ufw app list
```

vps need listing profile

```
Output
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

As demonstrated by the output, there are three profiles available for Nginx:

    **Nginx Full:** This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
    **Nginx HTTP:** This profile opens only port 80 (normal, unencrypted web traffic)
    **Nginx HTTPS:** This profile opens only port 443 (TLS/SSL encrypted traffic)

You can enable this by typing:

```
sudo ufw allow 'Nginx HTTP'
```

You can verify the change:

```
sudo ufw status
```

output

```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere              
Nginx HTTP                 ALLOW       Anywhere              
OpenSSH (v6)               ALLOW       Anywhere (v6)         
Nginx HTTP (v6)            ALLOW       Anywhere (v6)

```

### Step 3: Recheck nginx

```
systemctl status nginx
```

### Step 4: Some commands are used frequently

Restart nginx

```
nginx -s reload
```

or

```
systemctl restart nginx
```

Certbot

```
certbot --nginx -d domain.com
certbot delete --cert-name domain.com
```

config new domain on nginx
`/etc/nginx/sites-available/`

## III. Nginx monitoring

- Config nginx.conf enable `stub_status`
- or sử dụng Grafana + Prometheus + exporter => Cần cài `exporter`
- Ngoài ra còn một số cách khác của Grafana và ELK cần tham khảo thêm

## III. HTTP Basic Authentication

Tham khảo: 

- Apache basic authentication

  - [Link tham khảo từ blog.vinahost.vn](https://blog.vinahost.vn/http-basic-authentication/)
  - [Link tham khảo từ ubiq.co](https://ubiq.co/tech-blog/how-to-configure-basic-authentication-in-nginx/)
  - [Link tham khảo từ cyberciti](https://www.cyberciti.biz/faq/nginx-password-protect-directory-with-nginx-htpasswd-authentication/)
  - [Link tham khảo từ digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-22-04)
