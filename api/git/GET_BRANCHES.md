## Get Branches

{% method %}

Get all the branches of a Git project.

```
GET /api/project/<project id>/branches?n=<limit>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `n` | the maximum number of branches will return. |

Occasionally, a project could have a huge amount of branches, in which case,
loading them all could cause performance issues. You can use `n` param 
to control the number of banches will return.

In a successful response, the `branches` field contains all the branches.
Each branch has the following fields:

| field | description |
|:-:|---|
| `name` | (short) name of the branch |
| `full_name` | the full name of the branch in git database |
| `revision` | the SHA revision of the last commit in this branch |
| `timestamp` | the timestamp of the last commit in this branch |
| `ref_type` | the type of this reference. For branch, this is always `1`. |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/branches?n=5"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "branches": [
    {
      "name": "yarn-native-services",
      "full_name": "refs/heads/yarn-native-services",
      "revision": "34aeea7dff322952135140df090baaf1952efdd6",
      "timestamp": 1498069975,
      "ref_type": 1
    },
    {
      "name": "branch-2.8",
      "full_name": "refs/heads/branch-2.8",
      "revision": "81eb06b553cba5e80c469af2bcbbe2d95ad3d7f3",
      "timestamp": 1498063685,
      "ref_type": 1
    },
    {
      "name": "branch-2",
      "full_name": "refs/heads/branch-2",
      "revision": "d4115d71b5e776c05b3da59b8ad29ad0bb6b8a2c",
      "timestamp": 1498061112,
      "ref_type": 1
    },
    {
      "name": "trunk",
      "full_name": "refs/heads/trunk",
      "revision": "e806c6e0ce6026d53227b51d58ec6d5458164571",
      "timestamp": 1498061021,
      "ref_type": 1
    },
    {
      "name": "HDFS-7240",
      "full_name": "refs/heads/HDFS-7240",
      "revision": "b9a6441e1b297dd5f6ee8eaebf7ec3f7ec34c019",
      "timestamp": 1498012355,
      "ref_type": 1
    }
  ]
}
```

{% endmethod %}