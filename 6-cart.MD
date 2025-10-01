User is a microservice responsible for user login and registration service.
Developer choosen nodejs with version > 18.

Disable nodejs version that is less than 20.
```
dnf module disable nodejs -y
```
Enable the nodejs version 20
```
dnf module enalbe nodejs:20 -y
```
Install the nodejs
```
dnf install nodejs -y
```
Configure the application
Add Application user
```
useradd roboshop
```
Setup the app directory
```
mkdir app
```
Download application code to create app directory
```
curl -L -o /tmp/cart.zip https://roboshop-builds.s3.amazonaws.com/cart.zip
```
Change to app directory and extract
```
cd /app
```
```
unzip /tmp/cart.zip
```
Install the dependencies
```
npm install
```
Setup a systemd service so that systemctl can manage the service
```
vim /etc/systemd/system/cart.service
```
```
[Unit]
Description = Cart Service

[Service]
User=roboshop
Environment=MONGO=true
Environment=REDIS_HOST=<ip-address>
Environment=CATALOGUE_HOST=<Ip-address>
Environment=CATALOGUE_PORT=8080
ExecStart=/bin/node /app/server.js
SyslogIdentifier=cart

[Install]
WantedBy=multi-user.target
```
Load the service
```
systemctl daemon-reload
```
```
systemctl enable cart
```
```
systemctl start cart
```