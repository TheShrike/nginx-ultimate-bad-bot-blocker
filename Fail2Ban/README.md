# Fail2Ban Blacklist for Repeat Offenders of Nginx (action.d)

### Author: Mitchell Krog <mitchellkrog@gmail.com>
### Version: 1.1

# Add on for Nginx Ultimate Bad Bot blocker
GitHub: https://github.com/mitchellkrogza/nginx-ultimate-bad-bot-blocker


##### Tested On: Fail2Ban 0.9.3
##### Server: Ubuntu 16.04
##### Firewall: IPTables

### Dependancies: 
#####requires nginxrepeatoffender.conf in /etc/fail2ban/filter.d folder
#####requires nginxrepeatoffender.conf in /etc/fail2ban/action.d folder
#####requires jail settings called [nginxrepeatoffender]
#####requires nginx.repeatoffender file in /etc/fail2ban
`create with sudo touch /etc/fail2ban/nginx.repeatoffender`

`chmod +x /etc/fail2ban/nginx.repeatoffender`

#### Drawbacks: 
Only works with IPTables


#### Based on: 
The Recidive Jail from Fail2Ban

This custom filter and action for Fail2Ban will monitor your Nginx logs and perma-ban
any IP address that has generated far too many 444 or 403 errors over a 1 week period
and ban them for 1 day. This works like a charm as an add-on for my Nginx Bad
Bot Blocker which takes care of generating the 444 or 403 errors based on the extensive
list of Bad Referers, Bots, Scrapers and IP addresses that it covers. This provides short
block periods of one day which is enough to keep agressive bots from filling up your log files.
See - https://github.com/mitchellkrogza/nginx-ultimate-bad-bot-blocker for more info on the Nginx Bad Bot Blocker

This custom action requires a custom jail in your jail.local file for Fail2Ban

Your jail file would be configured as follows

```
[nginxrepeatoffender]
enabled = true
logpath = %(nginx_access_log)s
filter = nginxrepeatoffender
banaction = nginxrepeatoffender
bantime  = 86400   ; 1 day
findtime = 604800   ; 1 week
maxretry = 20
```

### If this helps you why not [buy me a beer](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=XP2AZ4S5HNAWQ):beer: