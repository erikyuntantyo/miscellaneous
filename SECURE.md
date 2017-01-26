## Minimize Connection to MongoDB using Iptables
```
iptables -A INPUT -p tcp -s OFFICE_PUBLIC_IP --dport LOCAL_MONGODB_PORT -j ACCEPT
iptables -A INPUT -p tcp -s 0.0.0.0/0 --dport LOCAL_MONGODB_PORT -j DROP
iptables -I INPUT -p tcp -s 127.0.0.1 --dport LOCAL_MONGODB_PORT -j ACCEPT

#allow connection from other server to backup database
iptables -I INPUT -p tcp -s STORAGE_IP --dport LOCAL_MONGODB_PORT -j ACCEPT
```

## Setup Fail2Ban
Goto [here](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-debian-7).

## Changes MongoDB Port
Changes the port within the configuration file:
* mongodb.conf

Changes the database connection configuration in each API service:
* GCM API (file: config.js)
* APN API (file: config.js)
* Chat API (file: config/connections.js)
* CMS API (file: config/connections.js)
* AsikPay API (file: config/connections.js)

> After all ports in the configurations changed, then restarts both **mongodb service** and **api services**.

## Set MongoDB User Account
Goto [here](https://www.cyberciti.biz/faq/how-to-secure-mongodb-nosql-production-database/)
