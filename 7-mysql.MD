# **Mysql**
Developer has choosen mysql database .
Install and configure mysql.
Developer has choosen mysql version 8.
```
dnf install mysql-server -y
```
Enable mysql
```
systemctl enable mysql
```
Start mysql
```
systemctl start mysql
```
Change the default root password inorder to start using the database service.
```
mysql_secure_installation --set-root-pass RoboShop@1
```
Check the root password in mysql 
```
mysql
```
