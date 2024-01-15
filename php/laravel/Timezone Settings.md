# Timezone Settings

## Example 1: Setup Timezone in Laravel.

Go to config/app.php file and search for 'timezone' and replace with below code:

```php
'timezone' => 'Asia/Kolkata',
```

## Example 2: Setup Timezone in laravel with env file:

Step 1: Go to **config/app.php** file, search for '`timezone`' and replace with the below code

```php
'timezone' => env('APP_TIMEZONE', 'UTC'),
```

## Step 2: Go to **`.env`** file and add the below code:

```conf
APP_TIMEZONE="Asia/Kolkata"
```

## Example 3: Setup Timezone in PHP:

```php
<?php
    date_default_timezone_set("Asia/Kolkata");   //India time (GMT+5:30)
    echo date('d-m-Y H:i:s');
?>
```
