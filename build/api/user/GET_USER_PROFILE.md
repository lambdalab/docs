## Get User Profile

{% method %}
This API returns the detail profile of current user.

```
GET /api/user/profile
```

A successful reponse contains the profile object with the following fields:

| field | description |
|:-:|---|
|`uid`| the id of current user |
|`display`| the display friendly name of the user |
|`name`| the name of the user |
|`email`| the email of the user |
|`avatarUrl`| the url of the user's image if exists |

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/user/profile?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "uid": "github@abc",
  "display": "abc",
  "name": "ABC",
  "email": "abc@gmail.com",
  "avatarUrl": "https://avatars3.githubusercontent.com/u/11"
}
```


{% endmethod %}

