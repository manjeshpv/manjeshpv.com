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


```sh
cd ~
git clone https://github.com/getsentry/onpremise.git sentry

cd sentry

./install.sh
```
