# Firewalld

**check status**
```
systemctl status firewalld
systemctl is-active firewalld 
firewall-cmd --state
```
**startup boot**
```
systemctl enable firewalld
systemctl is-enabled firewalld     #check
```
**restart**
```
systemctl restart firewalld
firewall-cmd --reload
```
**stop & disabled**
```
systemctl stop firewalld
systemctl disable firewalld
```
**config zones**
```
firewall-cmd --get-zones      #check list zones
firewall-cmd --get-default-zone     #check zone default
firewall-cmd --get-active-zones     #check zone active
firewall-cmd --set-default-zone-home  #set default zone home
firewall-cmd --zone=home --list-all   #check all rule of zone
firewall-cmd --zone=public --list services    #check services
firewall-cmd --zone=public --list-ports       #check ports
```
**identify services on system***
```
firewall-cmd --get-services
```

**disabled serivces on firewalld**
```
firewall-cmd --zone=public --remove-service=http
firewall-cmd --zone=public --remove-service=http  --permanent
```
**configure for port**
```
firewall-cmd –zone=public –add-port=80/tcp 
firewall-cmd –zone=public –add-port=80/tcp --permanent
```
**open range port**
```
firewall-cmd –zone=public –add-port=35000-40000/tcp
```
**close**
```
firewall-cmd --zone=public --remove-port=9999/tcp
firewall-cmd --zone=public --remove-port=9999/tcp --permanent
```
**create zone private**
```
firewall-cmd –permanent –new-zone=publicweb
firewall-cmd –permanent –new-zone=publicweb 
firewall-cmd –reload 
firewall-cmd –get-zones
```

**create services on firewalld**
- copy configure default & edit
```
cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/configurefirewall-admin.xml
nano /etc/firewalld/services/configurefirewall-admin.xml
```
![image](https://user-images.githubusercontent.com/69961900/208356939-a2b2f15b-7f8c-4980-bf5d-8b0898cdf690.png)
```
firewall-cmd –reload
```
**check list services**
```
firewall-cmd –get-services
```
**start services**
```
firewall-cmd –zone=public –add-services=configurefirewall-admin
firewall-cmd –zone=public –add-services=configurefirewall-admin –permanent
```
