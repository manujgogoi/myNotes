# Server Setup

## Hosting Account

- Provider: Hostinger.com (Global)
- Account: Google oAuth (manujgogoi@gmail.com)

## VPS

- Plan: KVM 2
- Expiration: 2026-03-31
- CPU Cores: 2
- Memory: 8 GB
- Bandwidth: 8 TB
- Disk Space: 100 GB
- IP: 91.108.111.136

## Settings-1:

- Operating System: Ubuntu 23.04 64bit
- Root Password: K\***\*\*\*\***#\*\*\*

### Connect VPS through SSH:

```sh
ssh root@91.108.111.136
```

> Issue: (WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!)
> Solution:

```sh
ssh-keygen -R <host_ip>
```

Output:

```sh
# Host 91.108.111.136 found: line 16
# Host 91.108.111.136 found: line 17
# Host 91.108.111.136 found: line 18
/Users/manuj/.ssh/known_hosts updated.
Original contents retained as /Users/manuj/.ssh/known_hosts.old
```

> Issue Closed

### Install NGINX

```sh
cat /etc/lsb-release
sudo apt update && sudo apt upgrade
sudo apt install nginx
sudo service nginx status # OR
systemctl status nginx
```

> `service` is adequate for basic service management, while directly calling `systemctl` give greater control options.

### Configure Firewall (UFW - UncomplicatedFireWall)

```sh
sudo ufw app list
```

- Now we will only need to allow traffic on port 80 (HTTP) and port 443 (HTTPS).

```sh
sudo ufw allow 'Nginx HTTP'
sudo ufw allow 'Nginx HTTPS'
```

- Now enable Firewall by typing:

```sh
sudo ufw enable
sudo ufw status
```

- Add and Delete firewall rules example:

```sh
sudo ufw allow ssh # Add Rule
sudo ufw delete allow ssh # Delete Rule
```

- Add Rule for OpenSSH

```sh
sudo ufw allow OpenSSH
sudo ufw status verbose
```

- Get VPS IP from vps terminal

```sh
curl ipinfo.io
{
  "ip": "91.108.111.136",
  "city": "Mumbai",
  "region": "Maharashtra",
  "country": "IN",
  "loc": "19.0728,72.8826",
  "org": "AS47583 Hostinger International Limited",
  "postal": "400070",
  "timezone": "Asia/Kolkata",
  "readme": "https://ipinfo.io/missingauth"
}
```

- Check Server Status
  On Browser: `http://your_vps_ip_address`

  Check from terminal

  ```sh
    curl 'http://91.108.111.136'
  ```

### Configure reverse proxy

- Create a new Nginx conf file for my company portfolio project using nextjs

```sh
vi /etc/nginx/sites-enabled/digilipi.conf
```

Paste the following

```sh
server {
    listen 80;
    root /var/www/digilipi/portfolio;
    server_name digilipi.com www.digilipi.com;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

- Remove the default conf file:

```sh
sudo rm /etc/nginx/sites-enabled/default
```

- Restart Nginx Server

```sh
# check nginx config
sudo nginx -t
# restart the nginx server
sudo service nginx restart
```

### Install NodeJS

- Step 1: Add Node.js 20 APT repository

```sh
sudo apt update

sudo apt install -y ca-certificates curl gnupg

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

NODE_MAJOR=20

echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

sudo apt update

```

- Step 2: Install Node.js

```sh
sudo apt install -y nodejs

node -v
npm -v
```

### Github Authentication

- Configure git on vps

1. git config

```sh
git config --list
git config --global user.name manujgogoi
git config --global user.email manujgogoi@gmail.com
git config --list # check configs
```

2. Generate ssh key

```sh
ssh-keygen -t ed25519 -C "manujgogoi@gmail.com"
```

- Enter custom name if required ('/root/.ssh/id_ed25519_github')

- Start the ssh-agent in the background.

```sh
eval "$(ssh-agent -s)"
```

- Add your SSH private key to the ssh-agent
  >

```sh
ssh-add ~/.ssh/id_ed25519_github
```

> Persisting ssh-add on system reboot
> Add the following code to the bottom of your `~/.bashrc` login file

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_github
```

3. Add SSH public key to github

- Copy ssh public key to clipboard

```sh
cat ~/.ssh/id_ed25519_github.pub
```

- Copy the output text
- In github go to [https://github.com/settings/keys](https://github.com/settings/keys)
- New SSH Key -> Add a title -> Paste the copy text in key section -> click Add SSH Key

- Check Connection

```sh
ssh -T git@github.com
```

4. Clone github project

- Go to `/var/www/digilipi/`
- Run the git clone

```sh
git clone git@github.com:digilipi/portfolio.git
```

### Install dependencies and run the project

Inside the portfolio directory

```sh
npm install
npm run dev # check for error
npm run build
# install pm2 globally
sudo npm install -g pm2
# Start Production build
sudo pm2 start npm --name "dl_portfolio" -- start
# Start pm2 on boot
sudo pm2 startup
# Save PM2 processes
sudo pm2 save
# If System reboots then type
sudo pm2 resurrect
```

### Add SSL Certificates

- Install Certbot
  > Certbot recommends using their snap package for installation.

```sh
sudo snap install core; sudo snap refresh core
# Remove older version of certbot
sudo apt remove certbot
# install the certbot package
sudo snap install --classic certbot
```

- Finally, you can link the certbot command from the snap install directory to your path, so you’ll be able to run it by just typing certbot.

```sh
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo ufw status
```

- delete the redundant Nginx HTTP profile allowance (Optional)

```sh
sudo ufw allow 'Nginx Full'
sudo ufw delete allow 'Nginx HTTP'
```

- Obtaining an SSL Certificate

```sh
sudo certbot --nginx -d digilipi.com -d www.digilipi.com
```

## Add a new User

```sh
adduser manuj
```

Add user to superuser (su) group

```sh
usermod -aG sudo manuj
```

Switch user

```sh
sudo su - manuj
```

---

# Reinstall Plain of Ubuntu 23.04 64bit

- Root Password: K****\*****#\*\*\*

## Connect VPS through SSH:

```sh
ssh root@91.108.111.136
ssh-keygen -R 91.108.111.136
ssh root@91.108.111.136
```

## Create a new user

```sh
adduser manuj
```

- FullName: Manuj Gogoi
- Password: M\***_#_**

### Add user to Superuser (sudo) group

```sh
usermod -aG sudo manuj
```

### Switch user

```sh
sudo su - manuj
```

## Nginx

```sh
sudo apt update && sudo apt upgrade
sudo apt install nginx
nginx -v
sudo service nginx status # OR
systemctl status nginx
```

## UFW

```sh
sudo ufw app list
sudo ufw status
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow 'Nginx Full'
sudo ufw delete allow ssh
sudo ufw allow OpenSSH
curl ipinfo.io
```

## Nginx Reverse Proxy settings

```sh
sudo rm /etc/nginx/sites-enabled/default
sudo vi /etc/nginx/sites-enabled/digilipi.conf
```

- Add the following content

```sh
server {
    listen 80;
    root /var/www/digilipi/portfolio;
    server_name digilipi.com www.digilipi.com;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```sh
sudo service nginx restart
```

## Install NodeJS (NVM)

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm -v
nvm ls-remote
nvm install v20.12.1
```

## Configure git and github

```sh
git config --list
git config --global user.name manujgogoi
git config --global user.email manujgogoi@gmail.com
git config --list # check configs

ssh-keygen -t ed25519 -C "manujgogoi@gmail.com"
```

Your public key has been saved in `/home/manuj/.ssh/id_ed25519_github.pub`

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_github
```

- Add the following code to the bottom of your `~/.bashrc` login file

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_github
```

- On github Settings add SSH key

```sh
ssh -T git@github.com # test connection
```

## Source Directory permissions

```sh
sudo mkdir /var/www/digilipi
sudo chown -R manuj:manuj /var/www/digilipi
cd /var/www/digilipi
git clone git@github.com:digilipi/portfolio.git
```

```sh
npm install
npm run dev # check for error
npm run build
# install pm2 globally
npm install -g pm2
npm install -g uuid@latest # (Optional) Deprecated warning
# Start Production build
pm2 start npm --name "dl_portfolio" -- start
# Save PM2 processes
pm2 save
# Start pm2 on boot
pm2 startup # copy output to startup script file ~/.bashrc
# If System reboots then type
pm2 resurrect # Optional
```

## Add SSL Certificates

```sh
sudo snap install core; sudo snap refresh core
# Remove older version of certbot
sudo apt remove certbot
# install the certbot package
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx
# OR
sudo certbot --nginx -d digilipi.com -d www.digilipi.com
```

# CI/ CD Pipeline

- github -> repo -> settings -> Actions -> runner -> new self hosted runner
- linux -> x64

## in VPS

```sh
mkdir actions-runner && cd actions-runner

curl -o actions-runner-linux-x64-2.314.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.314.1/actions-runner-linux-x64-2.314.1.tar.gz

echo "6c726a118bbe02cd32e222f890e1e476567bf299353a96886ba75b423c1137b5  actions-runner-linux-x64-2.314.1.tar.gz" | shasum -a 256 -c

tar xzf ./actions-runner-linux-x64-2.314.1.tar.gz

./config.sh --url https://github.com/digilipi/portfolio --token ADT43FJWEJ7MGJUBSRSJG2DGBXHU4

./run.sh

```

```sh
sudo ./svc.sh install
sudo ./svc.sh status
sudo ./svc.sh start
# To Stop
sudo ./svc.sh stop
```

- github -> repo -> Actions -> Search for node.js -> Select Node.js by github...
