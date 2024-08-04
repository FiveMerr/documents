# 🔄 DB Backups

Follow the instructions below to backup your database. You need to gather your details for your database and server details.&#x20;

## Backup Settings



{% hint style="info" %}
Name:&#x20;

Enter an easy to remember name for your reference. Use your RP server name.\
\
MySQL Host: \
This is your server IP's where your database is hosted (where xampp or MySQL installation is at)\
\
MySQL Port: \
Default port is usually 3306 but you may have a custom one. You will need to open these ports from your firewall to allow the connection. If you need to learn how to open your ports, you can visit [this](https://docs.1of1servers.com/1-of-1-knowledge-base/opening-your-ports) article to learn. You need to open port 3306 TCP incoming only. \
\
DO NOT OPEN YOUR PORTS WITHOUT ADDING A PASSWORD TO YOUR DATABASE OR ANYONE CAN SIMPLY JUST LOG INTO YOUR DATABASE.&#x20;
{% endhint %}

{% hint style="danger" %}
MySQL Database:\
You can go to your database viewer, usually HeidiSQL and see the name of it. Reference below. If you're using this for FiveM, you can usually find your database name on your server.cfg.

![](<../.gitbook/assets/image (1).png>)\
\
MySQL User: \
This is usually located on your FiveM server.cfg on the `mysql_connection_string` of your server.cfg by default it is usually root unless changed.&#x20;
{% endhint %}

{% hint style="danger" %}
MySQL Password: \
Your password for your database, usually this is set as no password therefore you need to set a password for your database. \
\
DO NOT OPEN YOUR PORTS WITHOUT ADDING A PASSWORD TO YOUR DATABASE OR ANYONE CAN SIMPLY JUST LOG INTO YOUR DATABASE. \
\
To add a password to your database open your database command prompt and run the below, replace `MyNewPasswordGoesHere` for the password you want to set on your server.\
\
Your server.cfg should then look something like this:&#x20;

```properties
set mysql_connection_string "mysql://root:MyNewPasswordGoesHere@localhost/QBCoreFramework_6EA45D?charset=utf8mb4"
```
{% endhint %}

```sql
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPasswordGoesHere'); FLUSH PRIVILEGES;
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
