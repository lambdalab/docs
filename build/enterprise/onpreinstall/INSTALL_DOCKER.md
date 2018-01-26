# Install Docker and Docker Compose

(**Outside of China**) If you have installed Docker and Docker Compose, you can skip this step. Otherwise You need to install Docker and Docker Compose first.

```bash
curl -sSL https://get.docker.com/ | sh
sudo usermod -aG docker $USER

sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

```

(**In China**) If you are in `China`, instead you could do:

```bash
curl -sSL https://get.daocloud.io/docker | sh
sudo usermod -aG docker $USER


sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

```

If this is first time you install Docker and Docker Compose, it is highly recommended to RESTART the machine before you continue: 

```bash
sudo reboot
```