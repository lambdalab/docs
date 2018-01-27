## Remove Admin User

{% method %}

This API allows the administrator of the system to revoke the administrator's permission of another
user in the system.

```
DELETE /api/admin/user/:userid
```

{% sample lang="http" %}
**Usage**
```bash
$ curl -v -X DELETE https://insight.io/api/admin/user/userpass@a@b.c?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "message" : "User: userpass@a@b.c removed as admin"
}
```

{% endmethod %}