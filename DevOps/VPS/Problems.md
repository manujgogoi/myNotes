# Problems:

## Problem

### 502 Bad Gateway

- Due to unknown reason my vps server had restarted and pm2 processes has not been accessing through proxy server (nginx)

### Solution:

```sh
pm2 stop dl_portfolio
pm2 delete dl_portfolio

# Project directory
cd /home/manuj/actions-runner/_work/portfolio/portfolio/
pm2 start npm --name "dl_portfolio" -- start
```
