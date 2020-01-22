# Installing sentry

Ubuntu 18

```sh
apt update

# set timezone https://askubuntu.com/questions/1198629/timezone-asia-kolkata-changed-to-pst
sudo apt-get remove tzdata
sudo apt-get install tzdata

# install docker https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04

sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

sudo apt update

sudo apt install docker-ce -y

sudo systemctl status docker

```
## installing docker compose - https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/

```sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

## installing onpremise
```sh
cd ~
git clone https://github.com/getsentry/onpremise.git sentry

cd sentry

./install.sh

docker-compose up -d
```

## Installing nginx
```sh
apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
cd /etc/nginx/conf.d
nano sentry.manjeshpv.com.conf

server {
 listen 80;
 server_name    sentry.manjeshpv.com default_server;
 client_max_body_size 20M;

  location / {
    proxy_redirect off;
    proxy_set_header   X-Real-IP         $remote_addr;
    proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Host              $http_host;
    proxy_pass http://127.0.0.1:9000;
  }
}
```

## Installing SSL

```sh
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update

sudo apt-get install certbot python-certbot-nginx -y
```


```sh

sudo certbot --nginx
```

## Adding SPF Record

```sh

curl ifconfig.me
# output: 123.123.123.123

# Create SPF in your DNS using spf generator https://www.spf-record.com/generator.php?domain=sentry.manjeshpv.com
Type: SPF
Name: sentry
Value: v=spf1 ip4:123.123.123.123 ~all
```
After entering check using https://www.kitterman.com/spf/validate.html?
