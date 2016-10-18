# PostgreSQL

`auto_explain`: [https://www.postgresql.org/docs/9.4/static/auto-explain.html](https://www.postgresql.org/docs/9.4/static/auto-explain.html)

* Installation: https://help.ubuntu.com/community/PostgreSQL
* Creating a user: http://stackoverflow.com/questions/11919391/postgresql-error-fatal-role-username-does-not-exist
* Set password: http://stackoverflow.com/a/7696398/914332
 
### Postgresql reset sequence

```sql
SELECT setval('cms_page_id_seq', (SELECT MAX(id) FROM cms_page));
```

### make dump of existing database

    $ pg_dump -O -U postgres database_name | gzip > /tmp/dump.sql.gz

### create dump without data

    $ pg_dump test_db_development -s > /tmp/createdb.sql

#### load database from dump

    $ psql -U username -f /tmp/dump.sql.gz
    $ psql -U username -d activar -f ~/Downloads/dump.sql

    $ sudo -u postgres psql db_development < ~/Downloads/dump.sql
    
### download as csv

```sql
\COPY enterprises TO '/tmp/empresas.csv' DELIMITER ';' CSV HEADER;
```

```sql
CREATE EXTENSION unaccent;
CREATE EXTENSION hstore;
```

#### allow user to acces tables, functions and sequences
```sql
GRANT ALL ON ALL TABLES IN SCHEMA public TO user;
GRANT ALL ON ALL FUNCTIONS IN SCHEMA public TO user;
GRANT ALL ON ALL SEQUENCES IN SCHEMA public TO user;
```

#### set password for all users as 'demo'
```sql
UPDATE auth_user set password ='bcrypt$$2a$12$udndek2c62VlLqWnAYU5qePYQ7SS9rmfnxIuGNhGR4EMfFadQsMuG';
```
or 
```sql
UPDATE userprofile_user set password ='bcrypt$$2a$12$udndek2c62VlLqWnAYU5qePYQ7SS9rmfnxIuGNhGR4EMfFadQsMuG';
```

#### First login as postgres user:

    $ sudo su - postgres

#### connect

    $ psql

#### show databases:

    \l

#### connect to the required db: 

    $ psql -d databaseName

#### show all tables:

    \dt

#### show columns:

    \d  social_auth_association

#### describe table:

    \d+ social_auth_association

#### rename constraint 
```sql
ALTER TABLE name RENAME CONSTRAINT constraint_name TO new_constraint_name;
```
#### create unique constraint
```sql
ALTER TABLE tablename ADD CONSTRAINT constraintname UNIQUE (columns);
```
#### Duplicate database 
```sql
CREATE DATABASE newdb WITH TEMPLATE olddb;
```
or

    $ createdb -T olddb newdb


# MySQL

    $ mysql

#### show all databases 

    mysql> SHOW DATABASES;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | test               |
    +--------------------+
    2 rows in set (0.00 sec)

    mysql> use test;

Database changed

    mysql> SHOW TABLES;
    +-----------------+
    | Tables_in_test  |
    +-----------------+
    | City            |
    | Country         |
    | CountryLanguage |
    | album           |
    | customer        |
    | item            |
    | numerics        |
    | sale            |
    | track           |
    +-----------------+
    9 rows in set (0.00 sec)

    mysql> CREATE DATABASE sales;
    mysql> DROP DATABASE sales;

#### get table structure

    mysql> DESCRIBE City;
    +-------------+----------+------+-----+---------+----------------+
    | Field       | Type     | Null | Key | Default | Extra          |
    +-------------+----------+------+-----+---------+----------------+
    | ID          | int(11)  | NO   | PRI | NULL    | auto_increment |
    | Name        | char(35) | NO   |     |         |                |
    | CountryCode | char(3)  | NO   |     |         |                |
    | District    | char(20) | NO   |     |         |                |
    | Population  | int(11)  | NO   |     | 0       |                |
    +-------------+----------+------+-----+---------+----------------+
    5 rows in set (0.00 sec)

#### count all the rows from table

    mysql> SELECT COUNT(*) FROM Country;
    +----------+
    | COUNT(*) |
    +----------+
    |      239 |
    +----------+
    1 row in set (0.01 sec)

    mysql> SELECT CONCAT("Hey ", title) FROM album;
    +----------------------------+
    | CONCAT("Hey ", title)      |
    +----------------------------+
    | Hey Two Men with the Blues |
    | Hey Hendrix in the West    |
    | Hey Rubber Soul            |
    | Hey Birds of Fire          |
    | Hey Live And               |
    | Hey Apostrophe             |
    | Hey Kind of Blue           |
    +----------------------------+
    7 rows in set (0.00 sec)

    mysql> SELECT CONCAT_WS(":", "1", 2, "3", "4");
    +----------------------------------+
    | CONCAT_WS(":", "1", 2, "3", "4") |
    +----------------------------------+
    | 1:2:3:4                          |
    +----------------------------------+
    1 row in set (0.00 sec)

    mysql> SELECT LPAD(title, 30, ' ') FROM album;
    +--------------------------------+
    | LPAD(title, 30, ' ')           |
    +--------------------------------+
    |         Two Men with the Blues |
    |            Hendrix in the West |
    |                    Rubber Soul |
    |                  Birds of Fire |
    |                       Live And |
    |                     Apostrophe |
    |                   Kind of Blue |
    +--------------------------------+
    7 rows in set (0.00 sec)

    mysql> SELECT RPAD(title, 30, ' ') FROM album;
    +--------------------------------+
    | RPAD(title, 30, ' ')           |
    +--------------------------------+
    | Two Men with the Blues         |
    | Hendrix in the West            |
    | Rubber Soul                    |
    | Birds of Fire                  |
    | Live And                       |
    | Apostrophe                     |
    | Kind of Blue                   |
    +--------------------------------+
    7 rows in set (0.00 sec)

#### Get counties that has no cities

    mysql> SELECT Name FROM Country WHERE Code NOT IN (SELECT DISTINCT CountryCode FROM City);
    +----------------------------------------------+
    | Name                                         |
    +----------------------------------------------+
    | Antarctica                                   |
    | Bouvet Island                                |
    | British Indian Ocean Territory               |
    | South Georgia and the South Sandwich Islands |
    | Heard Island and McDonald Islands            |
    | French Southern territories                  |
    | United States Minor Outlying Islands         |
    +----------------------------------------------+
    7 rows in set (0.31 sec)

#### numbre of cities for each country

    mysql> SELECT CountryCode, COUNT(CountryCode) FROM City GROUP BY CountryCode;
