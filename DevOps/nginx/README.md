# Basics

- A web server
- Proxy Server
- Load Balancer

## Nginx Configuration

- The main config file is typically named **"nginx.conf"** and is usually located in the **"/etc/nginx/"** folder
- Using a custom syntax comprising: `Directives` and `Blocks`

- This sets up the **Server's behaviour**

### Sample config

- Serving files itself
- Example of web server serving static files

```conf
server {
    listen: 80;
    server_name example.com www.example.com;

    location / {
        root /var/www/example.com;
        index index.html index.htm;
    }
}
```

- **location** directive defines how the server should process specific types of requests
- Specify the location that contains your files

### Forward Traffic to other web servers

```conf
server {
    listen: 80;
    server_name api.example.com;

    location / {
        proxy_pass http://backend_server_address;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### Sample Https configuration

- Serve Content over HTTPS with SSL/TLS configured

```conf
server {
    listen: 80;
    server_name example.com www.example.com;

    # Redirect all HTTP request to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name example.com www.example.com

    # SSL Configuration
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    # Security Headers
    add_header Strict-Transport-Security "max-age=31536000;includeSubDomains" always;

    location {
        root /var/www/example.com;
        index index.html index.htm;
    }
}
```

### Sample Configuration for Load Balancing

```conf
http {
    upstream myapp1 {

        server srv1.example.com;
        server srv2.example.com;
        server srv3.example.com;
    }

    server {
        listen: 80;
        location / {
            proxy_pass http://myapp1;
        }
    }
}
```

- In the example, there are 3 instances of the same app running on srv1-srv3
- All requests are proxied to the server group myapp1
- Defaults to **round-robin** algorithm;

## Worker Processes

- Controls how many parallel processes Nginx spawns to handle client requests
- Instead of using a new process for every incoming connection, nginx uses worker processes that handles many connections using a single-threaded event loop.
- The value is the number of worker processes Nginx should create.
- Each worker process runs independently and can handle its own set of connections
- This configuration directly influences how well it can handle traffic (performance)
- Should be tuned according to the server's hardware (CPU cores) and expected traffic load
- For a production build, it is generally recommended to create as many worker processes as there are CPU cores. This is based on the idea that each worker process can run independently, utilizing the full capacity of the available CPU resources without blocking other processes.

Example

```conf
workder_processes 1;
# worker_processes auto;
```

## Worker connections

- Per worker process: how many simultaneous connections can be opened
- Default is 512

Example

```conf
worker_processes 1;

events {
    worker_connections 1024;
}

```

- If you have 1 worker process, you will be able to server 1024 clients

## Contexts

> A few top-level directives, reffered to as contexts, group together the directives that apply to different traffic types:

- events: General connection processing
- http: HTTP traffic
- mail: Mail traffic
- stream: TCP and UDP Traffic

Directives placed outside of these contexts are said to be in the **_main context_**

Example:

```conf
worker_processes 1;

events {
    worker_connections 1024;
}

http {

}
```

### Inside http

- Server Block
  - Defines how Nginx should handle requests for a particular domain or IP address
  - How to listen for connections
  - which domain or subdomain the configuration applies to
  - How to route the requests

```conf
# ...

http {
    server {
        listen 8080;
        server_name localhost;

        location / {

        }
    }
}
```

### Inside server block

- **listen**: The IP address and port on which the server will accept requests
- **server_name**: Which domain or IP address this server block should respond to
- **location**: The root (/) URL, will apply to all requests unless more specific location blocks are defined

## Inside location block

- **proxy_pass**: Tells nginx to "Pass" the request to another server, making it act as a reverse proxy.

## Upstream Block

- Refers to servers that Nginx forwards requests to
- "upstream" name is based on the flow of data
- Upstream Servers = Refers to the traffic going from a client toward the source or higher-level infra, in this case application server
- Downstream Servers = Traffic going back to the client is "downstream"
- Upstream block defines a group of backend servers that will handle requests forwarded by by Nginx

Example:

```conf
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    upstream nodejs_cluster {
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }

    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://nodejs_cluster
        }
    }
}
```

## Forward info from the original client requests to the backend servers

### Original client requests:

- Original **IP Address**
- Original **Host**
- Referrer information
- Custom Headers

```conf
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    upstream nodejs_cluster {
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }

    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://nodejs_cluster
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

## We need to tell Nginx to include the corresponding MIME types in the "content-type" response header, when sending a file

> This helps the client understand how to process or render the file

```conf
worker_processes 1;

events {
    worker_connections 1024;
}

http {

    include mime.types;

    upstream nodejs_cluster {
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }

    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://nodejs_cluster
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

## Load balancing algorithms

```conf
# Other confs
http {
    # Other confs
    upstream nodejs_cluster {
        least_conn;
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }
    # Other confs
}
```

## Nginx commands

```bash
nginx # start nginx
nginx -h # Get options
nginx -s reload # Restart Nginx
nginx -s stop # Stop Nginx
tail -f /usr/local/var/log/nginx/access.log # print logs
mkdir ~/nginx-certs # create folder for nginx certificates
cd ~/nginx-certs
# create self-signed certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout nginx-selfsigned.key -out nginx-selfsigned.crt
```

## Final Nginx conf file:

```conf
# Main context (this is the global configuration)
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    include mime.types;

    # Upstream block to define the Node.js backend servers
    upstream nodejs_cluster {
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }

    server {
        listen 443 ssl;  # Listen on port 443 for HTTPS
        server_name localhost;

        # SSL certificate settings
        ssl_certificate /Users/nana/nginx-certs/nginx-selfsigned.crt;
        ssl_certificate_key /Users/nana/nginx-certs/nginx-selfsigned.key;

        # Proxying requests to Node.js cluster
        location / {
            proxy_pass http://nodejs_cluster;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }

    # Optional server block for HTTP to HTTPS redirection
    server {
        listen 8080;  # Listen on port 80 for HTTP
        server_name localhost;

        # Redirect all HTTP traffic to HTTPS
        location / {
            return 301 https://$host$request_uri;
        }
    }
}

```
