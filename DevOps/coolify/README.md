# Basics

> **Coolify** is a modern, **open-source**, **self-hosted** control panel designed to simplify the deployment and management of applications and databases. With Hostinger's "Ubuntu 24.04 with Coolify" VPS template, Coolify comes preinstalled, allowing you to quickly start managing your applications with ease.

## Step 1

- Ubuntu 24.04 with Coolify
- Root Password: K\***\*\*\*\***#\*\*\*

## Step 2 - Register

- `http://91.108.111.136:8000/register`
- Name: Manuj Gogoi
- Email: manujgogoi@gmail.com
- Password: D**\*\*\***#\*\*\*

## Step 3 - Settings

- **Settings** > **Configuration** > **Instance Settings**
  Put Insatance Domain - `https://coolify.digilipi.com` and Instance Name - `Digilipi` and press **Save**

## Step 4 - Create the Subdomain (Hostinger KVM Account)

## For WildCard Subdomain

> The \* (wildcard) A Record matches all subdomains of a domain that are not explicitly defined in DNS. It is used to point any undefined subdomains to a specific IP address.

```
Type = A
Name = *
Points To = 91.108.111.136
TTL = 60

```

## For Specific Subdomain

- In **hpanel.hostinger.com** / **domain** / **DNS / Nameservers** create an `A` Record

```
Type = A
Name = coolify
Points To = 91.108.111.136
TTL = 14400

```

## Step 5 - Set wildcard domain

- In **Servers** / **General** section set **Wildcard Domain** to `https://digilipi.com`
- **Save**

## Step 6 - Two Factor Authentication

- Recovery code:

```
n5w9Wx53ZQ-DZMVLe1Lal
EJWrQZUmfB-H0PcondzmX
Fx1Vl9UPL4-nD0z6ldL4n
MaGhM05mPO-wXY8If58Go
lIZAFpGXw7-lsijhUKNVc
HZRXpJSvCO-6xOMijjTXm
AQk1MGb1Rd-IhAPpLEfZb
TuQEM5llqF-W4CBuo4UJc
```

## Step 7 - Deploy Private Github Repo

- In **Sources** -> **Add**
- **New Github App**

```
Name: coolify-digilipi-portfolio
Organization: digilipi
```

- **Continue**
- Set Webhook Endpoint to `Use https://coolify.digilipi.com` (Https)
- Press **Register Now**
- Install \*\*coolify-digilipi-portfolio
- Only select repositories
- digilipi/portfolio
- press **Install**
