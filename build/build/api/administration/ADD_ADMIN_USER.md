## Add Admin User

{% method %}

This API allows the administrator of the system to grant the administrator's permission to another
user in the system.


```
POST /api/admin/user/:userid
```

{% sample lang="http" %}
**Usage**
```bash
$ curl -v -X POST https://insight.io/api/admin/user/userpass@a@b.c?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "message" : "User: userpass@a@b.c added as admin"
}
```

{% endmethod %}