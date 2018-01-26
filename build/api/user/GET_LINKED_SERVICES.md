## Get User Linked Services

{% method %}
This API returns services linked to current user.

```
GET /api/user/linkedservices
```

The `services` fields in a successful reponse is an array of all linked services' names.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/user/linkedservices?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "services": ["github","github-private"]
}
```

{% endmethod %}