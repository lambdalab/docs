## Remove Project

{% method %}

This API allows the administrator of the system to remove a Git repository from Insight.io.

```
DELETE /api/admin/project/<project id>
```

`project id` is the ID of the repository.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v -X POST https://insight.io/api/admin/project/github.com/apache/commons-logging?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
```

{% endmethod %}