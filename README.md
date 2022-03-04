# demo-webapp

A memo app containing multiple vulnerabilities.

Fuzzing Framework [shfz](https://github.com/shfz) is set in this repository, and you can fork this and try fuzzing.

check [scenario](https://github.com/shfz/demo-webapp/blob/main/fuzz/scenario.ts) and [Actions workflow](https://github.com/shfz/demo-webapp/blob/main/.github/workflows/fuzzing.yml).

## Try Fuzzing

1. Fork this repository.
2. Go to `Settings` -> `General` -> `Features` -> enable `Issues`.
3. Go to `Actions` -> enable workflows.
4. Go to `Actions` -> `Workflows` -> `All workflows` -> `fuzzing`, click `Run workflow` button, select `Branch: main`, and click green `Run workflow` button.
5. Fuzzing is started, and report is posted on issue.

## Memo app

### setup

```
$ docker-compose build
$ docker-compose up -d
```

> Database does not respond to initialization processing for about 30 seconds after startup.

### Command

#### Docker

- build to image

```
$ docker-compose build
```

- run containers

```
$ docker-compose up -d
```

- stop containers

```
$ docker-compose stop
```

- delete containers

```
$ docker-compose rm
```

- show logs

```
$ docker-compose logs
```

- rebuild and restart service

```
$ docker-compose stop
$ docker-compose rm
$ docker-compose build
$ docker-compose up -d
```

- When initializing the database (Erase all data, Change schema, Change username and password)

```
$ docker-compose stop
$ docker-compose rm
$ rm -rf ./db/data
$ docker-compose up -d
```

#### Database

- connect

```
# install mysql-client
$ sudo apt install -y mysql-client

# connect mysql
$ mysql -u root -p -h 127.0.0.1 -P 3306 --protocol=tcp
Enter password:
```

- query

```
mysql> use flask_db;
mysql> insert into users (username, password) values ('test', '111111');
mysql> select * from users;

+----+----------+----------+
| id | username | password |
+----+----------+----------+
|  1 | test     | 111111   |
+----+----------+----------+

mysql> insert into memos (user, title, text) values ('test', 'test-memo', 'test{this_is_test_memo}');
mysql> select * from memos;

+----+------+-----------+-------------------------+
| id | user | title     | text                    |
+----+------+-----------+-------------------------+
|  1 | test | test-memo | test{this_is_test_memo} |
+----+------+-----------+-------------------------+
```
