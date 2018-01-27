## Get Tags

{% method %}

Get all the tags of a Git project.

```
GET /api/project/<project id>/tags?n=<limit>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `n` | the maximum number of tags will return. |

Occasionally, a project could have a huge amount of tags, in which case,
loading them all could cause performance issues. You can use `n` param 
to control the number of tags will return.

In a successful response, the `tags` field contains all the tags.
Each tag has the following fields:

| field | description |
|:-:|---|
| `name` | (short) name of the tag |
| `full_name` | the full name of the tag in git database |
| `revision` | the SHA revision of the commit, to which this tag points |
| `timestamp` | the timestamp of the commit, to which this tag points  |
| `ref_type` | the type of this reference. For tag, this is always `2`. |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/tags?n=5"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "tags": [
    {
      "name": "rel/release-2.8.1",
      "full_name": "refs/tags/rel/release-2.8.1",
      "revision": "1e6296df38f9cd3d9581c8af58a2a03a6e4312be",
      "timestamp": 1496867878,
      "ref_type": 2
    },
    {
      "name": "rel/release-3.0.0-alpha3",
      "full_name": "refs/tags/rel/release-3.0.0-alpha3",
      "revision": "7c0489beb9fdf12e223a9e57779d3fef765a44d2",
      "timestamp": 1495682734,
      "ref_type": 2
    },
    {
      "name": "YARN-5355-branch-2-2017-04-25",
      "full_name": "refs/tags/YARN-5355-branch-2-2017-04-25",
      "revision": "3f3e926ba97532d78778b4abf61654a6e4fd48f1",
      "timestamp": 1493201612,
      "ref_type": 2
    },
    {
      "name": "YARN-5355-2017-04-25",
      "full_name": "refs/tags/YARN-5355-2017-04-25",
      "revision": "193746245bc4ae190e6ce18e040d70d15391d425",
      "timestamp": 1493119165,
      "ref_type": 2
    },
    {
      "name": "YARN-5355-2017-05-25",
      "full_name": "refs/tags/YARN-5355-2017-05-25",
      "revision": "193746245bc4ae190e6ce18e040d70d15391d425",
      "timestamp": 1493119165,
      "ref_type": 2
    }
  ]
}
```

{% endmethod %}