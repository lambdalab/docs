## Token Revoke/Deletion

{% method %}
To delete or revoke an api access token, `DELETE /api/token` with the target token attached in the `X-Auth-Token`.

```
DELETE /api/token
```

{% sample lang="http" %}
**Usage**
```bash
$ curl -v --header "X-Auth-Token:<your api access token>" https://insight.io/api/token
```

{% common %}
**Response**

You will always get an `HTTP/1.1 200 OK` no matter whether your token is valid or not.

{% endmethod %}