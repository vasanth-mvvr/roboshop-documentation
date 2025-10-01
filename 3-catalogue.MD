# **Catalogue**
Catalogue is a micro service responsible to display the list of products  in roboshop application.

Developer choosen nodejs with version 20

Install nodejs check the default version is not the same as developer version disable the old version and enable the new version.

We can check the module list
```
dnf module list nodejs
```

To disable and enable the module
```
dnf module disable nodejs -y
dnf module enable nodejs:20 -y
```
Install nodejs
```
dnf install nodejs -y
```
Enable the service
```
systemctl enable nodejs
```
Start the service
```
systemctl start nodejs
```
check the status
```
systemctl status nodejs
```

Config the application manually as it is developed by the developer of the company.

Add application user
```
useradd roboshop
```
User roboshop is a  function / daemon user to run the application. 

Create directory
```
mkdir /app
```
Download the application code to created the app directory.
```
curl -o /tmp/catalogue.zip https://roboshop-builds.s3.amazonaws.com/catalogue.zip
```
Change directory
```
cd /app
```
Extract the code 
```
unzip /tmp/catalogue.zip 
```
Every application is developed by the team will have some common software that they use as libraries.The application also as a some dependencies.
Lets download dependencies
```
cd /app
npm install
```
We need to setup a systemd service to manage the service.
```
vim /etc/systemd/system/catalogue.service
```
```
[Unit]
Description = Catalogue Service

[Service]
User=roboshop
Environment=MONGO=true
Environment=MONGO_URL="mongodb://catalogue.vasanthreddy.space/catalogue"
ExecStart=/bin/node /app/server.js
SyslogIdentifier=catalogue

[Install]
WantedBy=user.target
```

Load the service
```
systemctl daemon-reload
```
Enable and start the catalogue
```
systemctl enable catalogue
```
```
systemctl start catalogue
```

* For this application to work fully functional we need to load the schema to the database.
* Schema is usually a part of application code 

We need to load schema fo that we should install mongodb client
To have it installed we can setup mongodb repo and mongodb-client

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
```
dnf install mongodb-mongosh -y 
```

Load the schema
```
mongosh --host mongo.vasanthreddy.space </app/schema/catalogue.js
```
Note : Need to update the server ip address in the frontend configuration. /etc/nginx/default.d/roboshop.conf
