# **MONGO DB**
* Developer has choosen mongodb database for the project 

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
Install Mongo db
```
dnf install mongodb-org -y
```
Enable the service
```
systemctl enable mongod
```
Start the service
```
systemctl start mongod
```
Usally the mongodb port opens with the local host (127.0.0.1), meaning this service can be accessed by the application but in our case we need to access with the another server (remote access), so we need to change the config .

Update in the file /etc/mongodb.conf from 127.0.0.1 to 0.0.0.0 which is public access

Edit in the file 
```
vim /etc/mongodb.conf
```

Restart the service
```
systemctl restart mongod
```



