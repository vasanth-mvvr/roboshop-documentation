# **Payment**
This server is responsible for payment roboshop e-commerce app.
Install python
```
dnf install python3.11 gcc python3-devel -y
```
configure the application
```
useradd roboshop
```
Download the application code
```
curl -L -o /tmp/payment.zip https://roboshop-builds.s3.amazonaws.com/payment.zip
```
Make directory
```
mkdir /app
```
```
cd /app
```
Extract files
```
unzip /tmp/payment.zip
```
Download dependencies
```
cd /app
```
```
pip3.11 install -r requirements.txt
```
Setup systemd service so that systemctl will manage it.
```
vim /etc/systemd/system/payement.service
```
```
[Unit] 
Description = Payment Service

[Service]
User=root
WorkingDirectory=/app
Environment=CART_HOST=<ip-address>
Environment=CART_PORT=8080
Environment=USER_HOST=<ip-address>
Environment=USER_PORT=8080
Environment=AMQP_HOST=<ip-address>
Environment=AMQP_USER=roboshop
Environment=AMQP_PASS=roboshop123

ExecStart=/usr/local/bin/uwsgi --ini payment.ini
ExecStop=/bin/kill -9 $MAINPID
SyslogIdentifier=Payment

[Install]
WantedBy=multi-user.target
```
Load Service
```
systemctl daemon-reload
```
Enable and Start Service
```
systemctl enable payment
```
```
systemctl start payment
```


