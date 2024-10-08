## Build postgre + pgadmin using Docker


put this recipe to `docker-compose.yml` and run it with `docker-compose up`

```yaml
version: '3.8'

services:  

  db:
    container_name: pg_container
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: test_db
    ports:
      - "5432:5432"
  pgadmin:
    container_name: pgadmin4_container
    image: dpage/pgadmin4
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: root
    ports:
      - "5050:80"
```

if you set `POSTGRES_HOST_AUTH_METHOD` in postgres environment to `trust`, then `POSTGRES_PASSWORD` is not required.

## psql command list

some most used commands

| command | description |
|---------|------------:|
|`psql -d database -U user -W` | connects to database under a specific user |
|`\l` | list available databases |
| `\dt` | list available tables |
| `\d table_name` | describe a table |
| `\dn` | list all schemes of the currently connected db |
| `\df` | list available functions in the current db |
| `\dv` | list available view |
| `\du` | list all users and their assign role |
| `\g` | execute the last command again |
| `\?` | know all available psql commands |
| `\h` | get help |
| `\H` | switch the output to the HTML format | 
| `\q` | exit psql shell | 
| `\c db_name` | switch database |

When you get a connection to PostgreSQL it is always to a particular database. To access a different database, you must get a new connection.

Using \c in psql closes the old connection and acquires a new one, using the specified database and/or credentials. You get a whole new back-end process and everything. (https://stackoverflow.com/questions/10335561/use-database-name-command-in-postgresql)

## Show all database from terminal

```
psql -U root -c "SELECT * FROM pg_database";
```
- `-U` is user 
- `-c` is command querry

some of query command can be seen in the table below

| query command | description |
|---------|------------:|
| `SELECT current_database()` | retrieve the current database version  |
| `SELECT version();` | retrieve the current version |
| `CREATE DATABASE db_name;` | create database |
| `CREATE TABLE colors (ColorID int, ColorName char(20));` | create table named 'colors' |
| `INSERT INTO colors VALUES (1, 'red'), (1, 'blue'), (1, 'green');` | insert data to table | 



## Create role with option

`CREATE ROLE <role_name> [option]`

list of option: https://www.postgresql.org/docs/current/sql-createrole.html

sample options:

- `SUPERUSER`
- `LOGIN`

## Restore dump file

`psql dbname < dumpfile`

source: https://www.postgresql.org/docs/current/backup-dump.html

## Drop role

`DROP ROLE <role_name>`

## PostgreSQL Native Data Types

from the most common:
1. Number 
    - *integer* with range -/+2 bilion, 
    - *smallint*
    - *bigint*
    - *numeric* or *decimal* (eg. 123.45 would require a `numeric(5,2)`)
    - *real* and *double precision* is for floating values or data science application
2. Character
    - *char(n)* the characters should fit _n_ number
    - *varchar(n)* with length max _n_
    - *text* is for blog post or article
3. Date/Time
    - *date* stores dates between 4713 BC and 5874897 AD
    - *time* will store time of day accurate to 1 microsecond
    - *timestamp* to record both time and date in one column
    - *timestamp with time zone* 
4. Monetary
5. Binary
6. Boolean
7. Geometric
etc...

## Run psql Commmand via Docker 🏠

### SELECT command

```
docker exec -ti container_name psql -U user_name -d database_name -c "SELECT * FROM table_name LIMIT 1"
```

### CREATE database

```
docker exec -ti container_name psql -U user_name -c "CREATE DATABASE database_name" 
```

### DROP database

```
docker exec -ti container_name psql -U user_name -c "DROP DATABASE database_name"
```

### SHOW all databases

```
docker exec -ti container_name  psql -U user_name -c "SELECT * FROM pg_database"
```

### CREATE TABLE
```
docker exec -it pg_container_no_pass psql -U postgres -d <db_name> -c "CREATE TABLE <table_name> (id SERIAL, name VARCHAR)"
```

### Restore database

- option 1

```
docker exec -i container_name psql -U user_name -d database_name < path/to/dump.sql
```

- option 2

```
cat dump_file.sql | docker exec -i container_name psql -U username -d dbname

```

### Backup database

- option 1

```
docker exec -t your-db-container pg_dumpall -c -U postgres > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

- option 2a (with specific db name)

```
docker exec -t your-db-container pg_dump -c -U postgres -d your-db-name > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

- option 2b

```
docker exec -t your-db-container pg_dump -U postgres -F c -d your-db-name > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

- option 2c
```
pg_dump -U <username> -d <database_name> -F p -b -v -f <nama_file_backup>.sql
```

Penjelasan opsi yang digunakan dalam perintah ini:

-U <username>: Menentukan nama pengguna PostgreSQL yang memiliki akses ke basis data yang akan dibackup.   
  
-d <database_name>: Menentukan nama basis data yang akan dibackup.    
  
-F p: Menggunakan format plain SQL untuk file backup. Ini memastikan bahwa file backup akan berisi perintah SQL yang dapat dieksekusi.   
  
-b: Termasuk perintah CREATE TABLE dalam file backup. Opsi ini memastikan bahwa struktur tabel akan disertakan dalam backup.     
  
-v: Menghasilkan output yang lebih detail selama proses backup.    
  
-f <nama_file_backup>.sql: Menentukan nama file untuk menyimpan hasil backup. Anda dapat mengganti <nama_file_backup> dengan nama file yang Anda inginkan.   
  
Pastikan Anda mengganti <username>, <database_name>, dan <nama_file_backup> dengan nilai yang sesuai sesuai dengan lingkungan Anda. Setelah menjalankan perintah ini, Anda akan memiliki file backup dalam format SQL yang mencakup perintah CREATE TABLE serta data dari basis data yang Anda backup.


Problem:
- https://stackoverflow.com/questions/36753568/postgresql-tables-exists-but-getting-relation-does-not-exist-when-querying
