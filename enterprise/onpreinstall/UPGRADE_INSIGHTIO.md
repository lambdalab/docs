# Upgrade Insight.io

Upgrading Insight.io is made easy, fast and version-controlled as we manage update process with lambda-docker git repository. The first step of upgrade is save you local config change by `git commit` or `git stash` and the do:

```bash
git pull --rebase
```

on the docker compose git repo.

Then as mentioned before, if just docker-compose file is changed,

```bash
./lambda-compose up -d
```

could automatically restart the outdated
services. However, when config files under `configs` directory changes, `docker-compose up -d` will not know
who to update, therefore, whenever changes are made to the config files, it is more safe to do

```bash
./lambda-compose restart
```

to let tasks in containers run with new configs.
