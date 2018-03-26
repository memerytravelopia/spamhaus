__
</pre>
## Spamhaus DROP List ##
 A shell script that grabs the latest Spamhaus ipv4 & ipv6 DROP Lists and adds them to ipsets and iptables/ip6tables rules. 

## Usage Debian with ipset & netfilter-persistent  ##

Place the files in /etc/iptables/ on your server.

# make the spamhaus.xx.ipset executable
chmod +x spamhaus.v4.ipset && chmod +x spamhaus.v6.ipset

# set it loose
sudo ./spamhaus.v4.ipset && sudo ./spamhaus.v6.ipset

# confirm the rules have been added
iptables -nL |grep spamhaus && ip6tables -nL |grep spamhaus

</pre>

## Automatic Updating ##
In order for the list to automatically update each day, you'll need to setup a cron job with crontab.
<pre>
# fire up the crontab (no sudo)
crontab -e

# run the script every day at 3am
0 3 * * * /etc/spamhaus.v4.ipset
0 3 * * * /etc/spamhaus.v6.ipset
</pre>


## Troubleshooting ##
If you need to remove all the Spamhaus rules, run the following:
<pre>
#ipset
ipset flush spamhaus.v4
ipset flush spamhaus.v6
</pre>
