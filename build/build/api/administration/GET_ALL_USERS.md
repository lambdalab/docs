## Get All Users

{% method %}

This API allows the administrator of the system to retrieve all the users in the system.

```
GET /api/admin/users
```

A successful response is an array of users in the system. Each of the user has the following 
fields:

| field | description |
|:-:|---|
|`uid`| The ID of the user |
|`registerDate`| The timestamp when the user is registered in the system |
|`loginDate`| The timestamp when the user is lastly logged in |
|`main`| The type of the user's main loggin indentity |
|`isAdmin`| Indicating if the user is an administrator or not |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/admin/project/find?url=https://github.com/apache/commons-logging.git&token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "uid": "userpass@a@b.c",
    "registerDate": 1499301802081,
    "loginDate": 1499301802081,
    "main": "userpass",
    "isAdmin": true
  },

  ...

  {
    "uid": "userpass@ymhzsu@gmail.com",
    "registerDate": 1499553472450,
    "loginDate": 1499750055390,
    "main": "userpass",
    "isAdmin": false
  }
]
```

{% endmethod %}