# OwnCloud - Rclone mount S3 Storage
**update & upgrade OS**
```
apt-get update
apt-get upgrade
```
**install docker**
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
**check version**
```
docker -v
```
**enable startup**
```
systemctl enable docker
```
**install docker-rcompose**
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
**check version**
```
docker-compose --version
```
**install rclone + s3**
```
curl https://rclone.org/install.sh | sudo bash
```
**rclone config**
```
rclone config
```
**config file "/root/.config/rclone/rclone.conf" not found - using defaults </br> No remotes found, make a new one?**
```
n) new remote
s) set configuration password 
q) quit config  
n/s/q> n

Enter name for new remote
name> s3

5 / Amazon S3 Compliant Storage Providers including AWS, Alibaba, Ceph, China Mobile, Cloudflare...
Storage> 5

Next step 
> 24


```
