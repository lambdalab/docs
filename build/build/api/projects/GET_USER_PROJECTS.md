## Get All User Projects

{% method %}

This API will list all the project owned by current user from all linked service providers (e.g. GitHub, GitLab, LDAP). 

```
GET /api/user/projects
```

A successful response is an array of object. Each object has the following fields:

| field | description |
|:-:|---|
|`identity_name`| the name of the service provider |
|`projects`| all the projects of this user from this service provider |
|`status`| the status of this service provide for this user |

The `projects` field contains an array of `ProjectInfo`. The `status` field is an enumeration with the following values:

| value | description |
|:-:|-----|
|`0`| NOT_AUTHORIZED |
|`1`| ACCESS_DENIED |
|`2`| SUCCESSFUL |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/user/projects?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
[
  {
    "identity_name": "github",
    "projects": [
	  {
        "id": "github.com/apache/hadoop",
        "name": "hadoop",
        "remote_url": "https://github.com/hadoop/hadoop",
        "branch": "",
        "language": "Java",
        "is_private": false
      },
      
      ...

      {
        "id": "github.com/apache/spark",
        "name": "spark",
        "remote_url": "https://github.com/apache/spark",
        "branch": "",
        "language": "Scala",
        "is_private": false
      }
    ]
    "status": 2
  },
  {
    "identity_name": "github-private",
    "projects": [
	  {
        "id": "github.com/apache/hadoop",
        "name": "hadoop",
        "remote_url": "https://github.com/hadoop/hadoop",
        "branch": "",
        "language": "Java",
        "is_private": false
      },
      
      ...

      {
        "id": "github.com/apache/spark",
        "name": "spark",
        "remote_url": "https://github.com/apache/spark",
        "branch": "",
        "language": "Scala",
        "is_private": false
      }
    ]
    "status": 2
  },
  {
    "identity_name": "gitlab",
    "projects": [],
    "status": 0
  },
  {
    "identity_name": "ldap",
    "projects": [],
    "status": 0
  }
]
```

{% endmethod %}