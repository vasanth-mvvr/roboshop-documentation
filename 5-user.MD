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
curl -L -o /tmp/user.zip https://roboshop-builds.s3.amazonaws.com/user.zip
```
Change to app directory and extract
```
cd /app
```
```
unzip /tmp/user.zip
```
Install the dependencies
```
npm install
```
Setup a systemd service so that systemctl can manage the service
```
vim /etc/systemd/system/user.service
```
```
[Unit]
Description = User Service

[Service]
User=roboshop
Environment=MONGO=true
Environment=REDIS_HOST=<ip-address>
Environment=MONGO_URL="mongodb://<ip-address>:27017/users"
ExecStart=/bin/node /app/server.js
SyslogIdentifier=user

[Install]
WantedBy=user.target
```
Load the service
```
systemctl daemon-reload
```
```
systemctl enable user
```
```
systemctl start user
```
To work the application full functional we need to load the schema to the database
To load the schema we need to install mongo-db client.

Setting up and configuring mongodb repo file.
```
vim /etc/yum.repos.d/mongo.repo
```
```
[mongodb-org-8.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/8.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://pgp.mongodb.com/server-8.0.asc
```
Install the mongodb client
```
dnf install mongodb-mongosh -y
```
Load the schema
```
mongosh --host <url> </app/schema/user.js
```
