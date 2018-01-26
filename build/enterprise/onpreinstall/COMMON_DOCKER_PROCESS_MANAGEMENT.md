# Common Process Management with Docker Compose

`docker-compose` is a command line util to manage docker containers. It should be run under the folder where the `docker-compose.yaml` exists. We added a simple wrapper around it called `lambda-compose` to set all enviroment variables properly.
Common operations are as follows:

### List process


```bash
./lambda-compose ps
```

### Start whole Insight.io enterprise stack

```bash
./lambda-compose up -d
```

which is equivalent to use

```bash
./lambda-compose -f docker-compose.yml up -d
```

### Start a particular services

```bash
./lambda-compose up -d $service
```

### Sttach to a all containers' output

```bash
./lambda-compose logs -f
```


### Attach to a container’s output

```bash
./lambda-compose logs -f $service
```


### Stop and then clean all the contains

```bash
./lambda-compose down
```


### Run command inside (similar to ssh)

```bash
./lambda-compose run $container /bin/bash
```


### Find help
There are also kill/restart/rm commands if needed. use

```bash
./lambda-compse help $command_name
```

to find more details.