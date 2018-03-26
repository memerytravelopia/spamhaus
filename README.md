__
</pre>
## Spamhaus DROP List ##
 A shell script that grabs the latest Spamhaus ipv4 & ipv6 DROP Lists and adds them to ipsets and iptables/ip6tables rules. 

## Usage Debian with ipset & netfilter-persistent  ##

Place the script in /etc/iptables/ on your server.

# make it executable
chmod +x spamhaus.sh

# set it loose
sudo ./spamhaus.sh

# confirm the rules have been added
sudo iptables -L Spamhaus -n
</pre>

## Automatic Updating ##
In order for the list to automatically update each day, you'll need to setup a cron job with crontab.
<pre>
# fire up the crontab (no sudo)
crontab -e

# run the script every day at 3am
0 3 * * * /etc/spamhaus.sh
</pre>


## Troubleshooting ##
If you need to remove all the Spamhaus rules, run the following:
<pre>
#ipset
ipset flush spamhaus.v4
ipset flush spamhaus.v6
#iptables
sudo iptables -F Spamhaus
sudo ip6tables -F Spamhaus
</pre>
