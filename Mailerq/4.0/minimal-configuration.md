# A minimal configuration

MailerQ is configured via one central configuration file `config.txt` that can 
be found in the `/etc/mailerq` directory. It holds many options that you can
set before you start MailerQ. The most important options are the address
and login credentials of your RabbitMQ message broker, and the address of
your database. You probably need to change this setting. All other config 
file settings have decent defaults that work directly (although you might
want to take a look at them in a later stage).


## RabbitMQ address

The `rabbitmq-address` setting in the config file holds the address of the
RabbitMQ server that you want to use for message queueing. It has the
format "amqp://user:password@hostname/vhost". The default value 
("amqp://guest:guest@localhost/") only works if your RabbitMQ server
is running on the same machine as MailerQ, and when you've not altered
the default guest/guest credentials.

```
rabbitq-address: amqp://user:password@hostname/vhost
```

If you have a [cluster of RabbitMQ nodes](https://www.rabbitmq.com/clustering.html), 
the hostname can be separated by semi-colons (e.g. amqp://user:password@host1;host2;host3/vhost). 
Setting up a RabbitMQ cluster means you're less likely to loose message when
one RabbitMQ server fails.


## Database address

MailerQ stores all runtime settings in a relational database. This can be a Mysql,
MariaDB, PostgreSql or Sqlite3 database. The Sqlite3 database is by far the
easiest one to set up, because it does not require a running database server
and contains just the path to a file where MailerQ can store its runtime settings.

```
database: sqlite///path/to/database/file.sql
```

When MailerQ first connects to a database (or first opens the database file),
it automatically creates all database tables and initializes everything.

