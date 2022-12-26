# CSF 
- **Open a Port in CSF Firewall** </br>
**Open the configuration file of the CSF as follows.**
```
vi /etc/csf/csf.conf
```
**Add the required ports to the csf.conf file**
```
# Allow incoming TCP ports

TCP_IN = “20,21,22,25,26,53,80,110,143,443,465,587,993,995”

# Allow outgoing TCP ports

TCP_OUT = “20,21,22,25,26,37,43,53,80,110,113,443,465,873”
```
**Restart the CSF for the changes to take effect. Run the below command to restart the CSF.**
```
csf -r 
```

| Command	 | Description	 | Example |
| :---         |     :---:      |          ---: |
| csf -e	   | Enable CSF	     | root@server[~]#csf -e    |
| csf -x	     | Disable CSF	      | root@server[~]#csf -x      |
| csf -s	   | Start the firewall rules	     | root@server[~]#csf -s    |
| csf -f	     | Flush/Stop firewall rules (note: lfd may restart csf)| root@server[~]#csf -f      |
| csf -r	   | Restart the firewall rules	     | root@server[~]#csf -r    |
| csf -a [IP.add.re.ss] [Optional comment]	     | Allow an IP and add to /etc/csf/csf.allow       | root@server[~]#csf -a 187.33.3.3 Home IP Address      |
| csf -td [IP.add.re.ss] [Optional comment]	   | Place an IP on the temporary deny list in /var/lib/csf/csf.tempban	     |root@server[~]#csf -td 55.55.55.55 Odd traffic patterns    |
| csf -tr [IP.add.re.ss]	     | Remove an IP from the temporary IP ban or allow list.| root@server[~]#csf -tr 66.192.23.1      |
| csf -tf	   | Flush all IPs from the temporary IP entries   | root@server[~]#csf -tf    |
| csf -d [IP.add.re.ss] [Optional comment]	     | Deny an IP and add to /etc/csf/csf.deny	       | root@server[~]#csf -d 66.192.23.1 Blocked This Guy      |
| csf -dr [IP.add.re.ss]	   | Unblock an IP and remove from /etc/csf/csf.deny	     | root@server[~]#csf -dr 66.192.23.1   |
| csf -df    | Remove and unblock all entries in /etc/csf/csf.deny	      | root@server[~]#csf -df      |
| csf -g [IP.add.re.ss]   | Search the iptables and ip6tables rules for a match (e.g. IP, CIDR, Port Number)	       | root@server[~]#csf -g 66.192.23.1      |
| csf -t    |  Displays the current list of temporary allow and deny IP entries with their TTL and comments	       |  root@server[~]#csf -t      |
