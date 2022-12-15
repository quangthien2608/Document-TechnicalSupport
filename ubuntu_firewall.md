# Firewall
- **Configure file location**
```
sudo nano /etc/default/ufw
```
Edit
```
IPV6=yes
```

- **Deny incoming & allow outgoing**
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

- **Allow SSH connection**
```
sudo ufw allow ssh
```
or
```
sudo ufw allow 22
```
- **SSH with port 2222***
```
sudo ufw allow 2222
```

- **Enable UFW**
```
sudo ufw enable
```

- **Allow some connection**
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
