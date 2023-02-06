# Firewall
**Configure file location**
```
sudo nano /etc/default/ufw
```
Edit
```
IPV6=yes
```

**Deny incoming & allow outgoing**
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Allow SSH connection**
```
sudo ufw allow ssh
```
or
```
sudo ufw allow 22
```
**SSH with port 2222***
```
sudo ufw allow 2222
```

**Enable UFW**
```
sudo ufw enable
```

**Allow some connection**
**HTTP - 80**
```
sudo ufw allow http
```
or
```
sudo ufw allow 80
```

**HTTPS - 443**
```
sudo ufw allow https
```
or
```
sudo ufw allow 443
```

**Range 6000:6007/tcp & udp**
```
sudo ufw allow 6000:6007/tcp
sudo ufw allow 6000:6007/udp
```

**IP**
```
sudo ufw allow from 203.0.113.4
```
**IP connection with port 22 SSH**
```
sudo ufw allow from 203.0.113.4 to any port 22
```

**Subnets**
```
sudo ufw allow from 203.0.113.0/24
sudo ufw allow from 203.0.113.0/24 to any port 22
```

**Network Interface**
```
sudo ufw allow in on ens3 to any port 80
sudo ufw allow in on eth1 to any port 3306
```

**Denying Connections**
```
sudo ufw deny http
sudo ufw deny from 203.0.113.4
```

**Deleteing Rules**
```
sudo ufw status numbered
```
```
sudo ufw delete 2
```
**By Actual Rule**
```
sudo ufw delete allow http
sudo ufw delete allow 80
```
**Checking UFW Status and Rules**
```
sudo ufw status verbose
```
**Disabling or Resetting UFW**
**Disable**
```
sudo ufw disable
```
**Reset**
```
sudo ufw reset
```

