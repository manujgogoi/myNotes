# Php, MySQL, PhpMyadmin with brew

## Install PHP

```bash
brew services list
brew install php # Latest php = php8.4
# Install old versions
brew install php@8.2
brew unlink php # Change php version
brew link phhp@8.2
```

## Location

```
ls /opt/homebrew/etc/php/
```

## Test Php

### Hello World

- Create a project dir
- Inside the directory, create a file `index.php`

```php
<?php
echo ("Hello World!");
```

- Open the terminal and cd to the project directory and run the following command:

```bash
php -S localhost:8000
```

- Now open the browser and type `localhost:8000`

### Php Version

- Create another file called `php-version.php`

```php
<?php

phpinfo();
```

- Type on browser `localhost:8000/php-version.php`

## Install MySQL

```bash
brew install mysql
brew services list
brew services start mysql
mysql_secure_installation
```

> Password: `12345678`

## Install `PhpMyadmin`

```bash
brew install phpmyadmin
# configure phpmyadmin
# sudo -ln -s /opt/homebrew/etc/phpmyadmin /opt/homebrew/share/phpmyadmin
```

## Run `phpmyadmin`

```bash
php -S localhost:8080 -t /opt/homebrew/share/phpmyadmin
```
