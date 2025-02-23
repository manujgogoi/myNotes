# Install `phpMyAdmin` via `Homebrew`

Run the following command:

```bash
brew install phpmyadmin
```

## 1. Start MySQL

Ensure MySQL is running:

```bash
brew services start mysql
```

## 2. Configure phpMyAdmin Apache/Nginx or Start with PHP Built-in Server

There are two ways to serve phpMyAdmin:

### 🔹 Option 1: Serve with PHP Built-in Server (Quick Setup)

If you don't have `Apache/Nginx` configured, use PHP’s built-in server:

```bash
mkdir -p ~/Sites/phpmyadmin
ln -s /opt/homebrew/share/phpmyadmin ~/Sites/phpmyadmin


cd ~/Sites/phpmyadmin
php -S 127.0.0.1:8080
```

Now open http://127.0.0.1:8080 in your browser. ✅

### 🔹 Option 2: Serve with Laravel’s Built-in Artisan Server

You can add a route in your Laravel app to access phpMyAdmin:

1. Open your Laravel project folder and create a phpmyadmin symlink:

```bash
ln -s /opt/homebrew/share/phpmyadmin public/phpmyadmin
```

Now access phpMyAdmin via:
`http://127.0.0.1:8000/phpmyadmin`
