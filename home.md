General documentation on all sorts of topics

# Python
# Django
# Database
## MySQL
#### Create user
    
    CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
#### Permissions

    GRANT SELECT,INSERT,UPDATE,DELETE ON db_name.* TO 'username'@'localhost';

Granting all permissions

    GRANT ALL ON db_name.* TO 'username'@'localhost';
    
Show users
    
    SELECT host, user, password FROM mysql.user;

Set password

    SET PASSWORD FOR 'username'@'localhost' = password('a-good-password');

Renaming a database (quick fix)

    mysqldump -u username -p -v old_db > old_db_dump.sql
    mysqladmin -u username -p create new_db
    mysql -u username -p new_db < old_db_dump.sql

Renaming a database (using pipes). This requires that an empty db exists

    mysqldump old_db -p | mysql -D new_db -p

## PSQL
#### Connect
    psql dbname username
#### Show tables
    \d
#### Show databases
    \l (note that's a lowercase L)
#### Show columns
    \d table
#### Describe table
    \d+ table

# SysOp
# Unix/Linux