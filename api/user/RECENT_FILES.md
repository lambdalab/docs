## User Recent Visited Files

Insight.io provides a set of APIs for end users to manage their recent visited files.

### Get All Recent Visited Files

{% method %}

This API lists all the recent visited file of a given user.

```
GET /api/user/recentFiles
```

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/user/recentFiles?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

A successful result is an array of recent visited file objects. Each object has the following fields:

| field | description |
|:-:|---|
|`id`| the project's id of the recent visited file |
|`name`| the project's name of the recent visited file |
|`timeStamp`| the timestamp when the file was visited by the user |
|`revision`| the revision of the visited file |
|`path`| the path of the visited file |

{% common %}
**Response**

```json
HTTP/1.1 200 OK
[
  {
    "id": "github.com/apache/arrow",
    "name": "arrow",
    "timeStamp": 1499115245358,
    "revision": "master",
    "path": "/"
  },
  {
    "id": "github.com/apache/commons-logging",
    "name": "commons-logging",
    "timeStamp": 1494824820657,
    "revision": "trunk",
    "path": "src/main/java/org/apache/commons/logging/Log.java"
  }
]
```

{% endmethod %}


### Add a Recent Visited File

{% method %}

This API add a recent visited file for a given user.

```
POST /api/user/project/<project id>/recentFile/<revision>/<path>
```

| param | description |
|:-:|---|
|`project id`| the id of the project |
|`revision`| the revision of the file |
|`path`| the path of the file. If this is empty, use the root directory `/`. |

A successful result contains the add recent visited file action's result, which has the following fields:

| field | description |
|:-:|---|
|`id`| the project's id of the recent visited file |
|`name`| the project's name of the recent visited file |

{% sample lang="http" %}
**Usage**

```bash
$ curl -v -X POST "https://insight.io/api/user/project/github.com/apache/commons-logging/recentFile/master/src/main/java/org/apache/commons/logging/Log.java?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "isLoggedIn":true,
  "result":true
}
```

{% endmethod %}

### Remove a Recent Visited File

{% method %}

This API remove a file from recent visited files for a given user.

```
DELETE /api/user/project/<project id>/recentFile/<revision>/<path>
```

| param | description |
|:-:|---|
|`project id`| the id of the project |
|`revision`| the revision of the file |
|`path`| the path of the file. If this is empty, use the root directory `/`. |

A successful result contains the removing recent visited file action's result, which has the following fields:

| field | description |
|:-:|---|
|`id`| the project's id of the recent visited file |
|`name`| the project's name of the recent visited file |

{% sample lang="http" %}
**Usage**

```bash
$ curl -v -X DELETE "https://insight.io/api/user/project/github.com/apache/commons-logging/recentFile/master/src/main/java/org/apache/commons/logging/Log.java?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "isLoggedIn":true,
  "result":false
}
```

{% endmethod %}

