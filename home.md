General documentation on all sorts of topics

# Git
See what files changed from the last commit

    git diff-tree --no-commit-id --name-only -r <hash>

# Python
# Django
## Django Compressor

    pip install django-compressor

Compiling with Googles Closure compiler http://closure-compiler.googlecode.com/files/compiler-latest.zip
Unpack into ``bin/`` folder of Django project.

Sample ``settings.py``


    #####################
    # DJANGO COMPRESSOR #
    #####################
    COMPRESS_URL = STATIC_URL
    COMPRESS_ENABLED = True
    COMPRESS_OFFLINE = False
    COMPRESS_CSS_FILTERS = [
        'compressor.filters.css_default.CssAbsoluteFilter',
        'compressor.filters.cssmin.CSSMinFilter',
        ]
    COMPRESS_JS_FILTERS = [
        'compressor.filters.closure.ClosureCompilerFilter',
        ]
    COMPRESS_CLOSURE_COMPILER_BINARY = 'java -jar ' + os.path.join(PROJECT_ROOT, 'bin/compiler.jar')

    COMPRESS_PRECOMPILERS = (
        ('text/coffeescript', 'coffee --compile --stdio'),
        ('text/x-scss', 'sass --scss --debug-info -I static/css/ {infile} {outfile}'),
    )
    COMPILER_FORMATS = {
        '.sass' : {
            'binary.path' : 'sass',
            'arguments' : '*.sass *.css'
        },
        '.scss' : {
            'binary.path' : 'sass',
            'arguments' : '*.scss *.css'
        }
    }

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


#### Resetting root password
	sudo /etc/init.d/mysql stop
	sudo mysqld --skip-grant-tables &
	mysql -u root mysql
	UPDATE user SET Password=PASSWORD('YOURNEWPASSWORD') WHERE User='root'; FLUSH PRIVILEGES; exit;

#### Pip + MySQL

	pip install MySQL-python

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

### Changing ownership

    for tbl in `psql -qAt -c "select tablename from pg_tables where schemaname = 'public';" mydbname` ; do
               psql -c "alter table $tbl owner to mypsqluser" shirts ;     done

### Changing password

    ALTER USER shirtsculture_db_user WITH PASSWORD 'password''

### Admin panel

    sudo -s; su - postgres; psql template1


## Redis
Start up

    redis-server

Connect

    redis-cli -h localhost -p <port> -a password

Delete all keys

    flushall

## Memcached

	sudo apt-get install memcached

	pip install python-memcached


# Nginx
Sample ``nginx.conf``

    user www-data;
    worker_processes 4;
    pid /var/run/nginx.pid;

    events {
      worker_connections 768;
    	# multi_accept on;
    }

    http {

    	##
    	# Basic Settings
    	##
    	sendfile on;
    	tcp_nopush on;
    	tcp_nodelay on;
    	keepalive_timeout 65;
    	types_hash_max_size 2048;
    	# server_tokens off;
    	# server_names_hash_bucket_size 64;
    	# server_name_in_redirect off;

    	include /etc/nginx/mime.types;
    	default_type application/octet-stream;

    	##
    	# Logging Settings
    	##
    	access_log /var/log/nginx/access.log;
    	error_log /var/log/nginx/error.log;

    	##
    	# Gzip Settings
    	##
    	gzip on;
    	gzip_disable "msie6";

    	# gzip_vary on;
    	# gzip_proxied any;
    	# gzip_comp_level 6;
    	# gzip_buffers 16 8k;
    	# gzip_http_version 1.1;
    	# gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

    	##
    	# nginx-naxsi config
    	##
    	# Uncomment it if you installed nginx-naxsi
    	##

    	#include /etc/nginx/naxsi_core.rules;

    	##
    	# nginx-passenger config
    	##
    	# Uncomment it if you installed nginx-passenger
    	##

    	#passenger_root /usr;
    	#passenger_ruby /usr/bin/ruby;

    	##
    	# Virtual Host Configs
    	##

    	include /etc/nginx/conf.d/*.conf;
    	include /etc/nginx/sites-enabled/*;
    }


    #mail {
    #	# See sample authentication script at:
    #	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
    #
    #	# auth_http localhost/auth.php;
    #	# pop3_capabilities "TOP" "USER";
    #	# imap_capabilities "IMAP4rev1" "UIDPLUS";
    #
    #	server {
    #		listen     localhost:110;
    #		protocol   pop3;
    #		proxy      on;
    #	}
    #
    #	server {
    #		listen     localhost:143;
    #		protocol   imap;
    #		proxy      on;
    #	}
    #}

# Vim
Autoindent 4 spaces

    set smartindent
    set tabstop=4
    set shiftwidth=4
    set expandtab

# Unix/Linux
## Virtualenvwrapper
In .bashrc

    # virtualenvwrapper
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python
    export WORKON_HOME=~/.envs
    if [ -f /usr/local/bin/virtualenvwrapper.sh ]; then
    source /usr/local/bin/virtualenvwrapper.sh
    fi

## Homebrew
``brew update`` fails

    cd `brew --repository`
    git reset --hard HEAD
    brew update
If that doesn't work, try

    cd `brew --repository`
    git reset --hard origin/master
    brew update

## Emacs
### Emacs Live
Installation

    bash <(curl -fksSL https://raw.github.com/overtone/emacs-live/master/installer/install-emacs-live.sh)

If chosing to create a custom pack then it will be created in ``~/.live-packs/username-pack/``

This name can be changed in ``~/.emacs-live.el``. This file defines where to look for user packs. A good idea would be to move this into the .live-packs-directory. Doesn't feel clean to have two emacs-related dotfiles outside .emacs.d/


## Python
Console thingies

    import readline
    import rlcomplete
    readline.parse_and_bind('tab: complete')
