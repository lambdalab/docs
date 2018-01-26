## List All Tokens

{% method %}
To view all existing api access token in your account, `GET /api/token` with any valid access token attached in the `X-Auth-Token`, just like calling any other REST api, which requires authentication.

```
GET /api/token
```

In the response, `created` is the timestamp when the token was first created. `lastUsed` is the timestamp when the token was used
most recently.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v --header "X-Auth-Token:<your api token>" https://insight.io/api/token
```
{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "uid":"ldap@user.0",
    "apiToken":"95e1110da97bf616d2e6838677f0275d73c5b",
    "created":1496357580959,
    "lastUsed":1496357580959
  },
  {
    "uid":"ldap@user.0",
    "apiToken":"c9d1a9dd3ec6fa0f41543071f1c98cc6b66a7",
    "created":1496358254649,
    "lastUsed":1496358254649
  }
]
```
{% endmethod %}