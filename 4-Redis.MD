* Redis is used for in-memory data storage (caching) and allows users to access the data of the database over API.
Install redis there is a rpm
```
dnf install redis -y
``` 
Usually the port is localhost which is accessed by the application so in our case we want access it from the another server so we need to change it to 0.0.0.0.
```
vim /etc/redis/redis.conf
```

Enable and start redis
```
systemctl enable redis
systemctl start redis
```
