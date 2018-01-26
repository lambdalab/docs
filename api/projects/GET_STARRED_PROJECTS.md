## Get User Starred (Favorite) Projects

{% method %}
This API returns all the projects current user starred (marked as favorite) and sorted based on the time of the star action. 

```
GET /api/user/starredProjects
```

A successful response is an array made of starred project item, each of which is structured as
below:

| field | description |
|:-:|---|
|`id`| the id of the project |
|`name`| the name of the project |
|`starredAt`| the timestamp of when the project has been starred by current user |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/user/starredProjects?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "id": "github.com/apache/commons-logging",
    "name": "commons-logging",
    "starredAt": 1498867454913
  },
  {
    "id": "github.com/apache/arrow",
    "name": "arrow",
    "starredAt": 1498865695278
  },

  ...

  {
    "id": "github.com/apache/hadoop",
    "name": "hadoop",
    "starredAt": 1498596499274
  }
]
```

{% endmethod %}