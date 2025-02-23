# VPS Server Setup

## Install OS

- Ubuntu 24.04
- Password: `K*********#***`

## Add SSH Key

> Add SSH key to securely connect your VPS using terminal

- Generate SSH Key
- Open Terminal and run the following command

```bash
ssh-keygen -t ed25519 -C "manujgogoi@gmail.com"

Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/manuj/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/manuj/.ssh/id_ed25519
Your public key has been saved in /Users/manuj/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:aZ93UXzvY03D+8m5dDIrFFvcX1C55ZhlERE8Af+uyFA manujgogoi@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|             .oBO|
|              o=+|
|             . XB|
|         .  . *oB|
|        S   E+.o*|
|       . . oo  ==|
|          +.. +==|
|           +.o+=*|
|            o.o=o|
+----[SHA256]-----+
```

- Passphrase: `iamtheone`

```bash
ls ~/.ssh
code ~/.ssh/id_ed25519.pub
```

- Copy the content and paste it in hostinger `SSH Key content` section.
- Provide a name `mykey`.
- In terminal

```bash
ssh-keygen -R 91.108.111.136
ssh root@91.108.111.136
# Enter passphrase : iamtheone
```

## Add A new user

```bash
adduser manujgogoi
```

- Password: `M****#***`
- Full Name: `Manuj Gogoi`
- Room Number: `140`

### Enable Sudo Permission

```bash
usermod -aG sudo manujgogoi
```

### Switch to the new user

```bash
su - manujgogoi
```

## Install `tmux` on vps

```bash
sudo apt install tmux
```

## Copy SSH Key to `manujgogoi` user on vps.

```bash
ssh-copy-id manujgogoi@91.108.111.136

# Output---------
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/manuj/.ssh/id_ed25519.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
manujgogoi@91.108.111.136's password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'manujgogoi@91.108.111.136'"
and check to make sure that only the key(s) you wanted were added.
```

- Now ssh directly to the unroot user

```bash
ssh manujgogoi@91.108.111.136
```

## Disable password authentication

```bash
manujgogoi@srv501984:~$ sudo vim /etc/ssh/sshd_config
# Update the followings

# ------- Change this ----------
# PasswordAuthentication yes
# to
PasswordAuthentication no

# ----------- Change this ----------
UsePam yes
# to
UsePAM no


# ----------- Change this ----------
PermitRootLogin yes
# to
PermitRootLogin no
```

## In hostinger vps

- `manujgogoi@srv501984:~$ sudo vim /etc/ssh/sshd_config.d/50-cloud-init.conf`

```bash
# From
PasswordAuthentication yes
# to
PasswordAuthentication no
```

- To apply these changes:

```bash
sudo systemctl reload ssh
```

## Check these changes

```bash
# Exit from ssh connection
ssh root@91.108.111.136

# Output
Enter passphrase for key '/Users/manuj/.ssh/id_ed25519':
root@91.108.111.136: Permission denied (publickey).
```

### Now the vps is HARDENED FROM SSH ATTACKS (Specially Bruteforce)

## Install Docker and Docker Compose

```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker ps
# If not started then run the following command
sudo systemctl enable docker
# Add user to the docker group
sudo usermod -aG docker manujgogoi
# Restart the ssh connection and run the following
docker ps # without sudo command
```

## Local Dev Setup (Skipped)

[Instructions](/DevOps/VPS/02/LocalDevSetup.md)

## Deploy NextJs App + Prisma + PostgreSQL using Docker

[Github Repo](https://github.com/digilipi/ne-updates)

```bash
ssh manujgogoi@91.108.111.136
# Enter passkey (dialog from matrix)

# Generate SSH key to access private github repo
ssh-keygen -t rsa -b 4096 -C "manujgogoi@gmail.com"
cat ~/.ssh/id_rsa.pub
# Copy the output (it starts with ssh-rsa)
```
