# always-forge-Shift / OxyCoin / Rise / Lwf
**AlwaysForge** is PHP forging fail-over for **Shift** cryptocurrency. It will monitor all your nodes in real-time and switch forging to best server available. It uses active (maybe a little too aggressive) approach and best practices.

##Version:
`1.0.0`

##Dependencies:
Script require **PHP** with **cURL** support and **Cron**. If you want to run it on hosting instead of VPS - one with **SLA 99.99%** is highly recommended.

##Installation:
**Remember to add your monitor's server IP to Shift config whitelist (for API and forging)!**

/ **Remember to remove the passphrase from your shift config.json !**
```
sudo apt-get install php-curl
sudo apt install php php-cli php-mbstring php-sqlite3
git clone https://github.com/mrgrshift/free-ssl-shift (ssl, or just use my easy-ssl easy-nginx guide)
git clone https://github.com/seatrips/always-forge
cd always-forge
cp -a config.json.example config.json
```
Edit `config.json` to your needs:
```
{
    "log_level": "info", // Log details level: debug, info, none
    "check_interval_sec": 1, // Checker will pause for that interval each loop
    "timeouts": {
        "request_sec": 3, // Timeout for cURL request, must be higher than connect_msec
        "connect_msec": 1000 // Timeout for cURL connection establishment
    },
    "delegate": {
        "address": "delegate_address", // Your delegate address
        "publicKey": "delegate_publicKey", // Your delegate public key
        "secret": "delegate_secret" // Your delegate secret
    },
    // List of servers, first server will have highest priority, last - lowest priority
    // Each server must have unique name! For your delegate security HTTPS connection is forced!
    "servers": [
        {
            "name": "mainnetnode-1 #1",
            "ip": "127.0.0.1",
            "port": 443
        },
        {
            "name": "mainnetnode-2 #2",
            "ip": "127.0.0.1",
            "port": 443
        }
    ]
}
```

Save config and test it:
```
php always_forge.php
```
If it works - add to your crontab `monitor_always_forge.sh` to run every minute, for example: `crontab -e`, then insert:
```
* * * * * bash /home/seatrips/always-forge/monitor_always_forge.sh
```
##use this for logfile control
```
@daily > /home/seatrips/always-forge/always_forge.log
```
##to check activity
```
tail -f always_forge.log | grep "Forging enabled"
```

##Enjoy increase of your delegate productivity. :)
Donation address 4miners: `16010222169256538112L`
made by 4miners, edited by seatrips for shift
