# yahapi-mysql-migrations

Executes migration files for MySQL.

# Install

```
npm install --save @yahapi/mysql-migrations
```

# Example

```js
import Migrations from '@yahapi/mysql-migrations';

const migrations = new Migrations({
  database: 'mysql_migrations',
  host: '127.0.0.1',
  port: 3306,
  user: 'test',
  password: 'test',
}, {});

migrations.run(`${__dirname}/migrations/*.js`);
migrations.on('log', (lvl, msg) => {
  console.log(`${lvl}: ${msg}`);
});
```

### Options

The signature `new Migrations(config)` accepts mysql connection options which are identical to [mysql.createPool()](https://github.com/mysqljs/mysql#pooling-connections). At a minimum `host`, `database`, `user` and `password` must be specified.

### Events

* `log` Emitted with two arguments; `(lvl, msg)`.

# Run tests

Run `docker-compose up` to start a MySQL server with correct table and user.

If you're not using docker-compose, make sure to have a running MySQL server on port 3306 with the following database setup:

```sql
CREATE DATABASE mysql_migrations;
CREATE USER 'mysql_migrations'@'%' IDENTIFIED BY 'mysql_migrations';
GRANT ALL PRIVILEGES ON mysql_migrations.* TO 'mysql_migrations'@'%' WITH GRANT OPTION;
```
