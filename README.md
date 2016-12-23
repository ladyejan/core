# fso
Freesewing development

## System Requirements
* PHP 7 (but PHP 5.6 will work, too)
* composer

## Installation

### composer
Taken from the composer installation page: https://getcomposer.org/download/
```
 php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
 php -r "if (hash_file('SHA384', 'composer-setup.php') === 'c32408bcd017c577ce80605420e5987ce947a5609e8443dd72cd3867cc3a0cf442e5bf4edddbcbe72246a953a6c48e21') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
 php composer-setup.php
 php -r "unlink('composer-setup.php');"
```

### fso
```
 git clone git@github.com:joostdecock/fso.git
 composer install
 composer dump-autoload -o
 copy htaccess to .htaccess
```

## First call
* Enter in your browser {domain}/docs/demo/

## Troubleshooting

### OSX

For apache. If you installed nginx yourself, you probably know what to do

#### /private/etc/apache2/httpd.conf (needs sudo to edit)
Uncomment:
```
 LoadModule php5_module libexec/apache2/libphp5.so
 LoadModule userdir_module libexec/apache2/mod_userdir.so
 Include /private/etc/apache2/extra/httpd-userdir.conf
```
Add a ServerName entry as appropriate:
```
 ServerName mymachine:80
```
#### /etc/apache2/extra/httpd-userdir.conf (needs sudo to exit)
Uncomment:
```
 Include /private/etc/apache2/users/*.conf
```
#### Create/edit /private/etc/apache2/users/USERNAME.conf
Add a Directory directive. For example:
```
 <Directory "/Users/USERNAME/Sites">
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny
    Allow from localhost
 </Directory>
```
'Sites' is the default, to avoid fiddling, add a symlink;
```
 ln -s `pwd`/docs/ ~/Sites
```
#### Restart apache
```
 sudo apachectl -k restart
```
 Navigate to http://127.0.0.1/~USERNAME/index.php
