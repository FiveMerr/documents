# 🔄 DB Backups

Follow the instructions below to backup your database. You need to gather your details for your database and server details. \
\
Backups for all regular members are every 4 days and have a max of 2 backups all together.&#x20;

## Backup Settings

{% hint style="info" %}
#### Name:

Enter a memorable name for your reference, such as the name of your RP server.

#### MySQL Host:

This is the IP address of the server where your database is hosted (where XAMPP or MySQL is installed).

#### MySQL Port:

The default port is usually 3306, but you may have a custom port. You need to open this port in your firewall to allow the connection. For instructions on how to open your ports, you can visit this article. Ensure you open port 3306 for TCP incoming only.

\
**IMPORTANT:** **DO NOT** open your ports without adding a password to your database, as this will allow anyone to log into your database.
{% endhint %}

{% hint style="danger" %}
MySQL Database:\
To find the name of your database, you can use a database viewer such as HeidiSQL. Refer to the example below for guidance. If you are using this for FiveM, you can typically find the database name in your `server.cfg` file.

![](<../.gitbook/assets/image (1).png>)\
\
MySQL User:\
You can typically find the MySQL user in the `mysql_connection_string` section of your FiveM `server.cfg` file. By default, it is usually set to `root` unless it has been changed.
{% endhint %}

{% hint style="danger" %}
MySQL Password: \
If it is currently unset (no password), you need to set a password for security reasons.



**IMPORTANT:** **DO NOT** open your ports without adding a password to your database, as it will allow anyone to log into your database.



To add a password to your database, open your database command prompt and run the following command, replacing `MyNewPasswordGoesHere` with the password you want to set:

```sql
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPasswordGoesHere');
FLUSH PRIVILEGES;

```

After setting a password, you need to configure your database to allow connections from outside your local machine. Open your database command prompt and run the following command, replacing `MyPasswordGoesHere` with your database password:

```sql
CREATE USER 'root'@'%' IDENTIFIED BY 'MyPasswordGoesHere';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

\
If this is for FiveM, your `server.cfg` should then be updated to include the following line with your new password.&#x20;

```sql
set mysql_connection_string "mysql://root:MyNewPasswordGoesHere@localhost/QBCoreFramework_6EA45D?charset=utf8mb4"
```
{% endhint %}

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

