# MySQL on MacOS using `Homebrew`

## Problem: mysql server is not started!

- Reinstall

```bash
brew services stop mysql
rm -rf /opt/homebrew/var/mysql
brew reinstall mysql
brew services start mysql
brew services list
```

## Verify `MySQL` is running

Verify MySQL is Running

```bash
mysql -u root
```

If it works, proceed to **_secure MySQL_**.
