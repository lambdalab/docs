## Create Project

{% method %}
This API allows the administrator of the system to add one or multiple Git projects into the system.

```
POST /api/admin/project
```

The body of this `POST` request supports the following fields

| field | description |
|:-:|---|
|`urls`| The Git clone urls of all the projects. Separated by new line. |
|`isPrivate`| (Optional) If `true`, mark all the projects as private projects. |
|`enableManualUpdate`| (Optional) If `true`, set all the projects included in `urls` to be updated manually. |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v \
  -H "Content-Type: application/json" \
  -d '{"urls":"https://github.com/apache/commons-logging.git","isPrivate":"false"}' \
  https://insight.io/api/admin/project?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
```


{% endmethod %}

