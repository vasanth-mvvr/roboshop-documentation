# **NGINX**
* The Web/Frontend is the 

Install nginx
```
dnf install nginx -y
```
Enable nginx and start nginx
```
systemctl enable nginx
```
```
systemctl start nginx
```
Remove the default nginx 
```
rm -rf /usr/share/nhinx/html/*
```
Download the frontend content
```
curl -o /tmp/web.zip https://roboshop-builds.s3.amazonaws.com/web.zip
```
Extract the frontend code
```
cd /usr/share/nginx/html
```
```
unzip /tmp/web.zip
```
Create a nginx reverse proxy configuration
```
vim /etc/nginx/default.d/roboshop.conf
```
```
proxy_http_version 1.1;
location /images/ {
    expires 5s;
    root /usr/share/nginx/html;
    try_files $uri /images/placeholder.jpg;
}
location /api/catalogue/ {proxy_pass http:<ip-address>//:8080/;}
location /api/user/ {proxy_pass http:<ip-address>//:8080/;}

location /health {
    sub_status on;
    access_log off;
}
```
* The local host needs to replaced with actual ip address.

Restart nginx service
```
systemctl restart ngnix
```


