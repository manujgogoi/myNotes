# Connect MySQL with `Laravel` app

```bash
mysql -u root
```

```sql
CREATE DATABASE laravel_db;
```

## Configure `.env` File

Edit your `.env` file inside your Laravel project:

```conf
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_db
DB_USERNAME=root
DB_PASSWORD=your_mysql_password
```

👉 Set DB_PASSWORD if you have a MySQL root password; otherwise, leave it empty.

## Clear Config Cache (Important)

After editing `.env`, clear the config cache:

```bash
php artisan config:clear
php artisan cache:clear
```

## Run Database Migrations

```bash
php artisan migrate
```

## Serve the Laravel App

```bash
php artisan serve
```
