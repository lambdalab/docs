## Get Blames

{% method %}

Get all the line blames of a given file.

```
GET /api/project/<project id>/blames/<revision>/<filepath>
```

| param | description |
|:-:|---|
| `project id` | the id of the project. |
| `revision` | the revision of the file. |
| `filepath` | the path of the file. |

In a successful response, the `blames` field contains all the blames.
Each blame has the following fields:

| field | description |
|:-:|---|
| `commit` | the details of the commit associated with the line |
| `line` | the line where this blame commit item begins. It will end before the `line` of the next blame. Starts from `0` |

For each `commit` field, it is structured as follows:

| field | description |
|:-:|---|
| `sha` | The SHA number of this commit |
| `hashcode` | The hash code of this commit |
| `email` | The email of the author |
| `timestamp` | The timestamp when this commit is created |
| `name` | The name of the author |
| `short_message` | The message of the commit |
| `parent_revisions` | The revisions of the parent commits of this commit. |



{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/blames/trunk/LICENSE.txt"
```

{% common %}
**Response**

In this following example response, The first blame starts from line `0` to
line `208`, while the second one starts from line `209` and to the end of 
the file.

```json
HTTP/1.1 200 OK
{
  "blames": [
    {
      "commit": {
        "sha": "c94ff0f240de583311c1bd73cf41d113ade75ebf",
        "hashcode": 1640559713,
        "email": "omalley@apache.org",
        "timestamp": 1242707438000,
        "name": "Owen O'Malley",
        "short_message": "HADOOP-4687 More moving around",
        "parent_revisions": [
          "5128a9a453d64bfe1ed978cf9ffed27985eeef36"
        ]
      },
      "line": 0
    },
    {
      "commit": {
        "sha": "098ae11e35e5342fc732087e009a402259f544bb",
        "hashcode": 1764450645,
        "email": "aajisaka@apache.org",
        "timestamp": 1465965014000,
        "name": "Akira Ajisaka",
        "short_message": "HADOOP-12893. Verify LICENSE.txt and NOTICE.txt. Contributed by Xiao Chen, Andrew Wang, and Akira Ajisaka.",
        "parent_revisions": [
          "7d521a29eed62c4329b16034375bd5fb747a92a9"
        ]
      },
      "line": 209
    }
  ]
}
```

{% endmethod %}