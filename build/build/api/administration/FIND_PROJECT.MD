## Find A Project

{% method %}
This API allows the administrator of the system to find one project in the system with its Git clone url.

```
GET /api/admin/project/find?url=<project url>
```

In the query string, provide the `url` param with `project url`. 

If find a matched project, you will get a `ProjectInfo`. `404 Not Found`, otherwise.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/admin/project/find?url=https://github.com/apache/commons-logging.git?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "id": "github.com/apache/commons-logging",
  "name": "commons-logging",
  "remote_url": "https://github.com/apache/commons-logging",
  "branch": "trunk",
  ...
  "scmtype": 0,
  "origin": 100,
  "description": "Mirror of Apache Commons Logging",
  "language": "Java",
  "owner": "apache",
  "is_private": false,
  "enable_manual_update": false
}
```


{% endmethod %}
