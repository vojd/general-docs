General documentation on all sorts of topics

# Python
# Django
# Database
## MySQL
#### Create user
    
    CREATE USER 'username' IDENTIFIED BY 'password';
#### Permissions

    GRANT SELECT,INSERT,UPDATE,DELETE ON db_name.* TO 'username'@'localhost';
Granting all permissions

    GRANT ALL ON db_name.* TO 'username'@'localhost';
    
# SysOp
# Unix/Linux