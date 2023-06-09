# Домашнее задание к занятию 4. «PostgreSQL»

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.
```
yaha@yahawork:~/postgres$ docker run --name postgresql \
    -e POSTGRES_PASSWORD=sapassword \
    -v $PWD/data:/var/lib/postgresql/data \
    -p 5432:5432 \
    -d postgres:13
```

Подключитесь к БД PostgreSQL, используя `psql`.
```
yaha@yahawork:~/postgres$ docker exec -it postgresql bash
root@c4e70a7c04cb:/#
root@c4e70a7c04cb:/# psql -U postgres
psql (13.11 (Debian 13.11-1.pgdg110+1))
Type "help" for help.
```

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:

- вывода списка БД,
```
root@c4e70a7c04cb:/# psql -U postgres
psql (13.11 (Debian 13.11-1.pgdg110+1))
Type "help" for help.
```
- подключения к БД,
```
postgres-# \connect postgres
You are now connected to database "postgres" as user "postgres".
postgres-# 
```

- вывода списка таблиц,
```
postgres-# \dtS
                    List of relations
   Schema   |          Name           | Type  |  Owner   
------------+-------------------------+-------+----------
 pg_catalog | pg_aggregate            | table | postgres
 pg_catalog | pg_am                   | table | postgres
 pg_catalog | pg_amop                 | table | postgres
 pg_catalog | pg_amproc               | table | postgres
 pg_catalog | pg_attrdef              | table | postgres
 pg_catalog | pg_attribute            | table | postgres
 pg_catalog | pg_auth_members         | table | postgres
 pg_catalog | pg_authid               | table | postgres
 pg_catalog | pg_cast                 | table | postgres
 pg_catalog | pg_class                | table | postgres
 pg_catalog | pg_collation            | table | postgres
 pg_catalog | pg_constraint           | table | postgres
 pg_catalog | pg_conversion           | table | postgres
 pg_catalog | pg_database             | table | postgres
 pg_catalog | pg_db_role_setting      | table | postgres
 pg_catalog | pg_default_acl          | table | postgres
 pg_catalog | pg_depend               | table | postgres
 pg_catalog | pg_description          | table | postgres
 pg_catalog | pg_enum                 | table | postgres
 pg_catalog | pg_event_trigger        | table | postgres
 pg_catalog | pg_extension            | table | postgres
 pg_catalog | pg_foreign_data_wrapper | table | postgres
 pg_catalog | pg_foreign_server       | table | postgres
 pg_catalog | pg_foreign_table        | table | postgres
 pg_catalog | pg_index                | table | postgres
 pg_catalog | pg_inherits             | table | postgres
 pg_catalog | pg_init_privs           | table | postgres
 pg_catalog | pg_language             | table | postgres
 pg_catalog | pg_largeobject          | table | postgres
 pg_catalog | pg_largeobject_metadata | table | postgres
 pg_catalog | pg_namespace            | table | postgres
 pg_catalog | pg_opclass              | table | postgres
 pg_catalog | pg_operator             | table | postgres
 pg_catalog | pg_opfamily             | table | postgres
 pg_catalog | pg_partitioned_table    | table | postgres
 pg_catalog | pg_policy               | table | postgres
 pg_catalog | pg_proc                 | table | postgres
 pg_catalog | pg_publication          | table | postgres
 pg_catalog | pg_publication_rel      | table | postgres
 pg_catalog | pg_range                | table | postgres
 pg_catalog | pg_replication_origin   | table | postgres
 pg_catalog | pg_rewrite              | table | postgres
 pg_catalog | pg_seclabel             | table | postgres
 pg_catalog | pg_sequence             | table | postgres
 pg_catalog | pg_shdepend             | table | postgres
 pg_catalog | pg_shdescription        | table | postgres
 pg_catalog | pg_shseclabel           | table | postgres
 pg_catalog | pg_statistic            | table | postgres
 pg_catalog | pg_statistic_ext        | table | postgres
 pg_catalog | pg_statistic_ext_data   | table | postgres
 pg_catalog | pg_subscription         | table | postgres
 pg_catalog | pg_subscription_rel     | table | postgres
 pg_catalog | pg_tablespace           | table | postgres
 pg_catalog | pg_transform            | table | postgres
 pg_catalog | pg_trigger              | table | postgres
 pg_catalog | pg_ts_config            | table | postgres
 pg_catalog | pg_ts_config_map        | table | postgres
 pg_catalog | pg_ts_dict              | table | postgres
 pg_catalog | pg_ts_parser            | table | postgres
 pg_catalog | pg_ts_template          | table | postgres
 pg_catalog | pg_type                 | table | postgres
 pg_catalog | pg_user_mapping         | table | postgres
(62 rows)

postgres-# 

```
- вывода описания содержимого таблиц,
```
postgres-# \dtS+
                                        List of relations
   Schema   |          Name           | Type  |  Owner   | Persistence |    Size    | Description 
------------+-------------------------+-------+----------+-------------+------------+-------------
 pg_catalog | pg_aggregate            | table | postgres | permanent   | 56 kB      | 
 pg_catalog | pg_am                   | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_amop                 | table | postgres | permanent   | 80 kB      | 
 pg_catalog | pg_amproc               | table | postgres | permanent   | 64 kB      | 
 pg_catalog | pg_attrdef              | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_attribute            | table | postgres | permanent   | 456 kB     | 
 pg_catalog | pg_auth_members         | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_authid               | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_cast                 | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_class                | table | postgres | permanent   | 136 kB     | 
 pg_catalog | pg_collation            | table | postgres | permanent   | 240 kB     | 
 pg_catalog | pg_constraint           | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_conversion           | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_database             | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_db_role_setting      | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_default_acl          | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_depend               | table | postgres | permanent   | 488 kB     | 
 pg_catalog | pg_description          | table | postgres | permanent   | 376 kB     | 
 pg_catalog | pg_enum                 | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_event_trigger        | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_extension            | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_foreign_data_wrapper | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_foreign_server       | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_foreign_table        | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_index                | table | postgres | permanent   | 64 kB      | 
 pg_catalog | pg_inherits             | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_init_privs           | table | postgres | permanent   | 56 kB      | 
 pg_catalog | pg_language             | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_largeobject          | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_largeobject_metadata | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_namespace            | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_opclass              | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_operator             | table | postgres | permanent   | 144 kB     | 
 pg_catalog | pg_opfamily             | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_partitioned_table    | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_policy               | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_proc                 | table | postgres | permanent   | 688 kB     | 
 pg_catalog | pg_publication          | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_publication_rel      | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_range                | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_replication_origin   | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_rewrite              | table | postgres | permanent   | 656 kB     | 
 pg_catalog | pg_seclabel             | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_sequence             | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_shdepend             | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_shdescription        | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_shseclabel           | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_statistic            | table | postgres | permanent   | 248 kB     | 
 pg_catalog | pg_statistic_ext        | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_statistic_ext_data   | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_subscription         | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_subscription_rel     | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_tablespace           | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_transform            | table | postgres | permanent   | 0 bytes    | 
 pg_catalog | pg_trigger              | table | postgres | permanent   | 8192 bytes | 
 pg_catalog | pg_ts_config            | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_ts_config_map        | table | postgres | permanent   | 56 kB      | 
 pg_catalog | pg_ts_dict              | table | postgres | permanent   | 48 kB      | 
 pg_catalog | pg_ts_parser            | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_ts_template          | table | postgres | permanent   | 40 kB      | 
 pg_catalog | pg_type                 | table | postgres | permanent   | 120 kB     | 
 pg_catalog | pg_user_mapping         | table | postgres | permanent   | 8192 bytes | 
(62 rows)

postgres-# 

```

- выхода из psql.
```
ostgres-# \q
root@c4e70a7c04cb:/# 

```

## Задача 2

Используя `psql`, создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления, и полученный результат.
```
yaha@yahawork:~/postgres$ docker cp ./test_dump.sql postgresql:/tmp
yaha@yahawork:~/postgres$ docker exec -it postgresql bash
root@c4e70a7c04cb:/# ls /tmp
test_dump.sql
root@c4e70a7c04cb:/# 
root@c4e70a7c04cb:/# psql -U postgres
psql (13.11 (Debian 13.11-1.pgdg110+1))
Type "help" for help.

postgres=# CREATE DATABASE test_database;
CREATE DATABASE
postgres=# \q
root@c4e70a7c04cb:/# psql -U postgres -f /tmp/test_dump.sql test_database
SET
SET
SET
SET
SET
 set_config 
------------
 
(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
ALTER TABLE
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 8
 setval 
--------
      8
(1 row)

ALTER TABLE
root@c4e70a7c04cb:/# 
root@c4e70a7c04cb:/# psql -U postgres
psql (13.11 (Debian 13.11-1.pgdg110+1))
Type "help" for help.

postgres=# \connect test_database
You are now connected to database "test_database" as user "postgres".
test_database=# 
test_database-# \dt
         List of relations
 Schema |  Name  | Type  |  Owner   
--------+--------+-------+----------
 public | orders | table | postgres
(1 row)

test_database=# analyze verbose public.orders;
INFO:  analyzing "public.orders"
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
ANALYZE
test_database=# select avg_width from pg_stats where tablename='orders';
 avg_width 
-----------
         4
        16
         4
(3 rows)

test_database=# 
```

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам как успешному выпускнику курсов DevOps в Нетологии предложили
провести разбиение таблицы на 2: шардировать на orders_1 - price>499 и orders_2 - price<=499.

Предложите SQL-транзакцию для проведения этой операции.
```
test_database=# create table orders1 (check (price > 499)) inherits (orders);
CREATE TABLE
test_database=# insert into orders1 select * from orders where price > 499;
INSERT 0 3
test_database=# create table orders2 (check (price <= 499)) inherits (orders);
CREATE TABLE
test_database=# insert into orders2 select * from orders where price <= 499;
INSERT 0 5
test_database=# delete from only orders;
DELETE 8
test_database-# \dt
          List of relations
 Schema |  Name   | Type  |  Owner   
--------+---------+-------+----------
 public | orders  | table | postgres
 public | orders1 | table | postgres
 public | orders2 | table | postgres
(3 rows)

test_database=# 
```

Можно ли было изначально исключить ручное разбиение при проектировании таблицы orders?
```
использовать Table Partitioning
```

## Задача 4

Используя утилиту `pg_dump`, создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

