# Docker Problem

> error pulling image configuration: download failed after attempts=6: dialing docker-images-prod.6aa30f8b08e16409b46e0173d6de2f56.r2.cloudflarestorage.com:443 container via direct connection because has no HTTPS proxy: connecting to docker-images-prod.6aa30f8b08e16409b46e0173d6de2f56.r2.cloudflarestorage.com:443: dial tcp: lookup docker-images-prod.6aa30f8b08e16409b46e0173d6de2f56.r2.cloudflarestorage.com: no such host. Same error. What should I do. I hadn't change anything since last working time.

> Docker is unable to download the image due to a DNS resolution issue or network problem. (Local Machine - Macbook Air)

## 1. Check Internet & DNS Resolution

Try running:

```bash
ping -c 4 google.com
```

If it fails, your internet connection might be down.

Next, test DNS resolution for Docker's image host:

```bash
nslookup docker-images-prod.6aa30f8b08e16409b46e0173d6de2f56.r2.cloudflarestorage.com
```

If this fails, your DNS might be blocking it. Try switching to a public DNS: `/etc/resolv.conf`

```bash
scutil --dns
```

Your system is using the following DNS servers:

- `2409:40e6:16:3dcd::b1` (IPv6)
- `192.168.119.90` (local network)

## Possible Issues:

1. Local DNS (`192.168.119.90`) Might Be **_Blocking Docker Requests_**

- This could cause failures in resolving Docker's image registry.

2. IPv6 DNS (`2409:40e6:16:3dcd::b1`) Might Be Causing Issues

- Some networks have issues resolving domains via IPv6.

## Solution: Change DNS to Public DNS

Try switching to Google's or Cloudflare's DNS.

### Step 1: Update DNS

Run this command to set your DNS servers to Google's (8.8.8.8, 8.8.4.4) and Cloudflare's (1.1.1.1):

```bash
sudo networksetup -setdnsservers Wi-Fi 8.8.8.8 8.8.4.4 1.1.1.1
```

> Note: If you're using Ethernet, replace `Wi-Fi` with `Ethernet` in the command.

Or edit `/etc/resolv.conf` manually:

```bash
sudo nano /etc/resolv.conf
```

Replace its content with:

```bash
nameserver 8.8.8.8
nameserver 8.8.4.4
nameserver 1.1.1.1
```

Save (`CTRL+X → Y → ENTER`).

To verify the change:

```bash
networksetup -getdnsservers Wi-Fi
```

It should return:

```bash
8.8.8.8
8.8.4.4
1.1.1.1
```

### Step 2: Flush DNS Cache

```bash
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```

### Step 3: Restart Docker on macOS

- Click on the **Docker** icon in the menu bar.
- Select **Quit Docker**.
  Reopen Docker from Applications or run:

```bash
open -a Docker
```

### Try Running Docker Compose Again

```bash
docker compose up --build
```
