## Get Typeahead Search Data

{% method %}
This API returns typeahead  search data `GET /api/search/datum`. You have to provide the following params in the url.

* `q`: Required. The query string, e.g. "config"
* `projectId`: Required. The project id the query is limited to, if project id is empty string "", the search will be across all projects
* `type`: Optional. Specify the type of result: 0 - all results, 1 - symbol nodes, 2 - file name, 3 - project name

A valid response contains an array of nodes, with each node having the following data structure:

| field | description |
|:-:|---|
|`value`| Qualified name for symbol node, file name for file node, project name for project node |
|`kind`| NodeKind of the Node, refer to [Meta Data](./INDEX.md) for `NodeKind` structure |
|`qualifier`| The qualifier of the node. |
|`identifier`| the identifier of the node |
|`projectId`| the project Id of the project the node belongs to  |
|`projectName`| the project name of the project the node belongs to  |
|`branch`| branch the node belongs to |
|`line`| the line where the node is located |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/getDatum?q=hadoop"
```


{% common %}
**Response**

```json
HTTP/1.1 200 OK
[
  {
    "value": "org.apache.hadoop.io.Writable",
    "tokens": [
      "org.apache.hadoop.io.Writable",
      "Interface"
    ],
    "kind": "Interface",
    "qualifier": "io.",
    "identifier": "Writable",
    "path": "src/java/org/apache/hadoop/io/Writable.java",
    "projectId": "github.com/cloudera/hadoop-common",
    "projectName": "hadoop-common",
    "branch": "trunk",
    "line": 65
  },

...

  {
    "value": "elasticsearch-hadoop",
    "tokens": [
      "elasticsearch-hadoop",
      "Project"
    ],
    "kind": "Project",
    "qualifier": "elasticsearch-hadoop",
    "identifier": null,
    "path": "",
    "projectId": "github.com/elastic/elasticsearch-hadoop",
    "projectName": "elasticsearch-hadoop",
    "branch": "master",
    "line": 0
  }
]
```


{% endmethod %}