# Cloudflare Dynamic DNS IP Updater
Update your domain records whenever your home IP changes to keep your self-hosted website accessible.

## Installation
On your linux machine (RasberryPi)

```
apt update && apt install git -y
git clone https://github.com/vlada-jerkovic/dynamicdns.git
cp cloudflare-template.sh cloudflare-updater.sh
cp cloudflare-templatev6.sh cloudflare-updaterIPv6.sh
nano cloudflare-updater.sh
chmod +x cloudflare-updater.sh
```

## Configure cron
Run script every minute
```
crontab -e
```
Add line with your path
```
*/1 * * * * /bin/bash /root/cloudflare-ddns-updater/cloudflare-updater.sh
```
Restart cron to start execution
```
systemctl restart cron
```

## Testing
1. Create in Cloudflare DNS subdomain **script** and set IP to 8.8.8.8

2. Inside script set record_name to subdomain script.[YOUR DOMAIN]

Results: It should modify 8.8.8.8 to your home IP.


## Usage

```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday 7 is also Sunday on some systems)
# │ │ │ │ │ ┌───────────── command to issue                               
# │ │ │ │ │ │
# │ │ │ │ │ │
# * * * * * /bin/bash {Location of the script}
```