## Get File Tree

{% method %}
We provide a flexible API, which can filter file trees by how deep the file tree goes
(`depth`) and where does the tree starts (`beginPath`).

```
GET /api/project/<project id>/directoryTree/<revision>/<beginPath>?depth=<depth>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `revision` | the revision of the project |
| `beginPath` | from which path the file tree expands. Optional. If not provided, `root` path is used. |
| `depth` | the maximum depth the file tree can go from `beginPath`.  |

The response has part of the entire directory tree. This partical tree still starts
from `root` directory, but will only contains the direct parent nodes of
`beginPath`. And then starts from `beginPath` node, it has all the children nodes with distance to the `beginPath` node not larger than `depth`.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/project/github.com/apache/commons-logging/directoryTree/trunk/src/main/assembly?depth=1"
```

{% common %}
**Response**

As you can see from the result, the file tree has the nodes starts from
`root`, but only has full children list when come to the requested path
`/src/main/assembly`. And after that, the tree only goes `1` step further
and then stops. 

```json
HTTP/1.1 200 OK
{
  "name": "",
  "path": "",
  "obj_type": 2,
  "children": [
    {
      "name": "src",
      "path": "src/",
      "obj_type": 2,
      "children": [
        {
          "name": "main",
          "path": "src/main/",
          "obj_type": 2,
          "children": [
            {
              "name": "assembly",
              "path": "src/main/assembly/",
              "obj_type": 2,
              "children": [
                {
                  "name": "bin.xml",
                  "path": "src/main/assembly/bin.xml",
                  "obj_type": 3,
                  "is_simple": false
                },
                {
                  "name": "src.xml",
                  "path": "src/main/assembly/src.xml",
                  "obj_type": 3,
                  "is_simple": false
                }
              ],
              "is_simple": false
            }
          ],
          "is_simple": false
        }
      ],
      "is_simple": false
    }
  ],
  "is_simple": false
}
```

{% endmethod %}