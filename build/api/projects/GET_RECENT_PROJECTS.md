## Get User Recently Visited Projects

{% method %}
This API returns all the projects current user visited and sorted based on the time of the visit. 

```
GET /api/user/recentProjects
```

A successful response is an array made of project visit item, each of which is structured as
below:

| field | description |
|:-:|---|
|`id`| the id of the project |
|`name`| the name of the project |
|`lastViewedAt`| the timestamp of when the project has been viewed by current user |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/user/recentProjects?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "id": "github.com/apache/commons-logging",
    "name": "commons-logging",
    "lastViewedAt": 1498867454913
  },
  {
    "id": "github.com/apache/arrow",
    "name": "arrow",
    "lastViewedAt": 1498865695278
  },

  ...

  {
    "id": "github.com/apache/hadoop",
    "name": "hadoop",
    "lastViewedAt": 1498596499274
  }
]
```

{% endmethod %}