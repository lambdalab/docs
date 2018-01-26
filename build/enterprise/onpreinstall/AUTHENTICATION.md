# Authentication


(**CentOS only**) For some Linux version such as CentOS, Docker may not be automatically running after system reboot, in which case you may need to restart Docker process manually first to proceed:

```bash
sudo systemctl start docker
```

(**Outside of China**) To be able to pull the images, you need log into docker hub with your user name which is already authorized by lambdalab
If you haven't got authorized, please send an email to lambdalab@lambdalab.io.

```bash
docker login
```

(**In China**) If you are in `China`, please use our private registry for better speed.

First, you need to register an account at 

`https://registry.lambdalab.io`

and ask lambdalab@lambdalab.io to authorize your account, then you need do

```bash
    docker login registry.lambdalab.io
```
