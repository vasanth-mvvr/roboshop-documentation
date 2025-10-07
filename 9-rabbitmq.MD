# **RabbitMQ**
RabbitMQ is message queue which is used by some componenets of applications.

A Yum repository with RabbitMQ packages is available from PackageCloud.
```
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash
```
RabbitMQ Erlang repository
```
 curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | sudo bash
```
Install RabbitMQ
```
dnf install rabbitmq-server -y
```
Enable and start rabbitMQ
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
RabbitMQ comes with default username and password as guest.This user cannot be used to connet. So create a username and password
```
rabbitmqctl add_user roboshop roboshop123
```
setting permissions
```
rabbitmqctl set_permissions -p / roboshop ".*" ".*" ".*"
```


