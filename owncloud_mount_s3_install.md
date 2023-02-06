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

provider> 24
env_auth>
access_key_id> input access key
secret_access_key> input secret access key
endpoint> s3-hcm-r1.longvan.net
location_constraint>
acl> 1

Edit advanced config?
y) Yes
n) No (default)
y/n> n

Keep this "s3" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y

```

**mount S3 config including Rclone**
**create folder S3 data mount s3 rclone**
```
mkdir –p /home/owncloud/own_data/files/
```
**create service rclone**
```
cd /etc/systemd/system/ 
wget https://s3-hcm1-r1.longvan.net/testing/rclone.txt
cp -r rclone.txt rclone.service
```
Environment=MOUNT_DIR=/home/owncloud/own_data/files/ is folder sync data server s3 rclone
```
systemctl restart daemon-reload
systemctl restart rclone
systemctl enable rclone
```
**create folder data owncloud**
```
mkdir -p /home/owncloud/own_data/db/
mkdir -p /home/owncloud/own_data/redis/
```

**create folder containt file install owncloud docker compose**
```
mkdir -p /home/owncloud/own_installer/own/
cd /home/owncloud/own_installer/own/
```
**get file docker-compose.yml**
```
wget https://s3-hcm1-r1.longvan.net/testing/docker-compose.yml
```
**create the environment configuration file**
```
cat << EOF > .env
OWNCLOUD_VERSION=10.11
OWNCLOUD_DOMAIN=localhost:8080
OWNCLOUD_TRUSTED_DOMAINS=IP server current using
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin
HTTP_PORT=8080
EOF
```

**installing**
```
cd /home/owncloud/own_installer/own/
docker-compose up -d
```
**check access owncloud** </br>
http://{your ip}:8080

