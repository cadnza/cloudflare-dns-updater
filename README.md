# `cloudflare-dns-updater`

![](https://img.shields.io/github/v/release/cadnza/cloudflare-dns-updater)

Updates a DNS record of your choosing in Cloudflare. Ideal for dynamic DNS.

## Details

Thing updates the IP of your target record to the IP obtained from `dynamicdns.park-your-domain.com/getip` every 3 minutes.

## Setup

### 1. Symlink this directory and the services it contains

```
sudo ln -s ~/Repos/cloudflare-dns-updater /etc/systemd/system/com.cadnza.cloudflare-dns-updater.service.d
sudo ln -s ~/Repos/cloudflare-dns-updater/com.cadnza.cloudflare-dns-updater.service /etc/systemd/system/
sudo ln -s ~/Repos/cloudflare-dns-updater/com.cadnza.cloudflare-dns-updater.timer /etc/systemd/system/
```

### 2. Reload the `systemctl` daemon to make it aware of the new files

```
sudo systemctl daemon-reload
```

### 3. Set environment variables

Configure the service

```
sudo systemctl edit com.cadnza.cloudflare-dns-updater.service
```

to define the following variables:

```
Environment="AUTH_EMAIL=[Your CloudFlare email]"
Environment="AUTH_KEY=[Your global API key]"
Environment="RECORD_IDENTIFIER=[The record identifier of the record you'd like to update]"
Environment="ZONE_IDENTIFIER=[The zone identifier of that record's zones]"
Environment="RECORD_NAME=[That record's name]"
```

### 4. Start the service

```
sudo systemctl enable com.cadnza.cloudflare-dns-updater.timer
sudo systemctl start com.cadnza.cloudflare-dns-updater.timer
```
