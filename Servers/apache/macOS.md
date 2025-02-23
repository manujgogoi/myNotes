# Apache on MacOS

## Built-In

### 1. Check Apache Status

```bash
sudo apachectl status

# Output
Go to http://localhost:80/server-status in the web browser of your choice.
Note that mod_status must be enabled for this to work.
```

If it says "not running", then Apache is not active.

### 2. Check if Apache is Running on Port 80

Use this command to see if Apache is running:

```bash
sudo lsof -i :80
```

- If no output appears, Apache is not running.
- If there is an entry like `httpd`, Apache is running.

### 3. Start Apache (If Not Running)

If Apache is not running, start it with:

```bash
sudo apachectl start
```

To restart Apache:

```bash
sudo apachectl restart
```

To stop Apache:

```bash
sudo apachectl stop
```

### 4. Verify Apache is Working

Once started, open a browser and go to:

```bash
http://localhost
```

If Apache is running, you should see the default "It works!" page.

### 5. Check Apache Version (Optional)

To check the installed version:

```bash
httpd -v
# Or
apachectl -v
# Output
Server version: Apache/2.4.62 (Unix)
Server built:   Dec 13 2024 23:45:22
```

### httpd.conf file

macOS includes a built-in version of Apache, and its `httpd.conf` file is located at:
`/etc/apache2/httpd.conf`

## Apache Using Homebrew

### 1. Stop Built in Apache

```bash
sudo apachectl stop
sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist
```

### 2. Install Apache using Homebrew

```bash
brew install httpd
```

### 3. Start Apache

```bash
brew services start httpd
```

### 4. Check status

> Built-in apache uses port 80 but homebrew apache uses 8080

```bash
curl -I http://localhost:8080 # For brew httpd
curl -I http://localhost:80 # for built in httpd
```

```bash
curl -I http://localhost:8080
# output
HTTP/1.1 200 OK
Date: Tue, 18 Feb 2025 07:45:34 GMT
Server: Apache/2.4.63 (Unix)
Last-Modified: Tue, 18 Feb 2025 07:34:35 GMT
ETag: "2d-62e65ac25d8c0"
Accept-Ranges: bytes
Content-Length: 45
Content-Type: text/html
```
