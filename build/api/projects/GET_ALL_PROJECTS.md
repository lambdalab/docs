## Get All System Projects

{% method %}
This API returns all the project included in the system, including both public and private projects. **Note**: This API requires Admin permission.

```
GET /api/admin/projects
```

A successful response is an array made of `ProjectInfo`s.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/admin/projects?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "id": "github.com/liuyangvip/weather",
    "name": "weather",
    "remote_url": "https://github.com/liuyangvip/weather",
    "branch": "master",
    "main_branch": "master",
    ...
    "scmtype": 0,
    "origin": 1,
    "language": "Java",
    "owner": "liuyangvip",
    "is_private": false
  },

  ...

  {
    "id": "github.com/matyhtf/webim",
    "name": "webim",
    "remote_url": "https://github.com/matyhtf/webim",
    "branch": "master",
    ...
    "scmtype": 0,
    "origin": 100,
    "description": "使用PHP+Swoole实现的网页即时聊天工具",
    "language": "JavaScript",
    "owner": "matyhtf",
    "is_private": false
  }
]
```

{% endmethod %}