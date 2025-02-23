# Install and uninstall on MacBook

```bash
brew install nginx
brew services start nginx
```

## Uninstall `nginx`

```bash
brew services stop nginx
brew uninstall nginx
brew uninstall --force nginx
rm -rf /usr/local/etc/nginx /usr/local/var/log/nginx /usr/local/var/run/nginx.pid
```

If you installed Homebrew on an Apple Silicon Mac (M1/M2/M3), the path may be different:

```bash
rm -rf /opt/homebrew/etc/nginx /opt/homebrew/var/log/nginx /opt/homebrew/var/run/nginx.pid
```

Ensure no NGINX processes are running:

```bash
ps aux | grep nginx
```

If any processes are still running, stop them using:

```bash
sudo pkill nginx
```

To remove any cached files:

```bash
brew cleanup
```

Check if NGINX is fully removed:

```bash
nginx -v
```

If it returns command not found, NGINX has been completely removed.
