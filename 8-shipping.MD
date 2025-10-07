# **Shipping**
Shipping service is responsible to finding the distance of the package to be shipped and calculate the price based on that .
Shipping service is written in java .
install java manven is the packaging software , Install the maven.
```
dnf install maven -y
```
configure the application
```
useradd roboshop
```
Install the application code
```
curl -L -o /tmp/shipping.zip https://roboshop-builds.s3.amazonaws.com/shipping.zip
```
Make directory app
```
mkdir /app
```
```
cd /app
```
Extract the application code
```
unzip /tmp/shipping.zip
```
Every application is developed by the developmnent team will have some common software that uses libraries.So the application also as some dependencies in the app cofiguration

Download the application and build the application
```
cd /app
```
```
mvn clean package
```
```
mv target/shipping-1.0.jar shipping.jar
```
Setup a systemd shipping service
```
vim /etc/systemd/system/shipping.service
```
```
[Unit]
Description = Shipping Service

[Service]
User=roboshop
Environment=CART_ENDPOINT=<cart ip-address>:8080
Environment=DB_HOST=<mysql ip-address>
ExecStart=/bin/java -jar /app/shipping.jar
SyslogIdentifier=shipping

[Install]
WantedBy=multi-user.target
```
Load the service
```
systemctl daemon-reload
```
Enable the service
```
systemctl enable shipping
```
Start the service
```
systemctl start shipping
```
For the application to work functional we need to load the schema to the database.
To load the schema we need to install mysql
```
dnf install mysql -y
```
Load Schema
```
mysql -h <ip-address> < /app/db/schema.sql
```
```
mysql -h <ip-address> < /app/db/app-user.sql
```
```
mysql -h <ip-address> < /app/db/master-data.sql
```
Restart the service
```
systemctl restart shipping
```


