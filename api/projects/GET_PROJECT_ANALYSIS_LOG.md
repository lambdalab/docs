## Get Project Analysis Log

{% method %}

This API allows you to get real-time project analysis console logs from Insight.io. By making 
repeated GET requests with a parameter,  you can retrieve in-progress console output. You'll 
basically send this `GET` request. The `start` parameter controls the byte offset of where you
start.


```
GET /api/project/<project id>/buildLog
```

The response will contain a chunk of the console output, as well as the `X-Text-Size` header
that represents the bytes offset (of the raw log file). This is the number you want to use
as the start parameter for the next call.

If the response also contains the `X-More-Data: true` header, the server is indicating that
the build is in progress, and you need to repeat the request after some delay. it's recommended
to wait after at least `5` seconds before make next call.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/project/github.com/apache/commons-logging/buildLog?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**

```
HTTP/1.1 200 OK
Started by user lambdalab-jenkins
Building remotely on jenkins-slave-0 in workspace /home/jenkins/workspace/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__
[commons-logging-lDbjfpnPYP9lpLOsHtUYcw__] $ /bin/sh -xe /tmp/hudson7776496668529108731.sh
+ rm -rf /home/jenkins/workspace/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__/../commons-logging-lDbjfpnPYP9lpLOsHtUYcw__-tmp
+ mkdir -p /home/jenkins/workspace/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__/../commons-logging-lDbjfpnPYP9lpLOsHtUYcw__-tmp
[commons-logging-lDbjfpnPYP9lpLOsHtUYcw__] $ /bin/sh -xe /tmp/hudson6773885465359779319.sh
+ git init
Initialized empty Git repository in /home/jenkins/workspace/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__/.git/
+ git fetch --depth=1 git://dataservice/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__ 276e55d980373100d2aedb83ef556cd795acee37
From git://dataservice/commons-logging-lDbjfpnPYP9lpLOsHtUYcw__
 * branch            276e55d980373100d2aedb83ef556cd795acee37 -> FETCH_HEAD
+ git checkout 276e55d980373100d2aedb83ef556cd795acee37
Note: checking out '276e55d980373100d2aedb83ef556cd795acee37'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

...

```


{% endmethod %}