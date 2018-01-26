## Get References

{% method %}

This API gets you all the references of a definition node.

```
GET /api/project/<project id>/metadata/references/<revision>/<signature>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `revision` | the revision of the project |
| `signature` | the id of the definition node |

In a successful response, it's structured as follows:

In the top level `references`, it's groupped by the reference type, e.g. `override`, `inherit`, etc.
In the example, it's has one group `10`, which is `override`. Each item in the array is wrapped
references in a project. The `project_info` field has the details of the project, the `references`
array contains all the references groupped by files in this project. Then each item in this array
contains all the references grouppped by a single file. The `file_loc` field contains the details of
the file, and the `references` array are the actual references in this particular file. Each
`reference` item in the array has the following structure:

| field | description |
|:-:|---|
|`lineno`| the line number of the reference usage, starts from `0` |
|`content`| the file content of this line |
|`range`| the offsets range in of the usage node in this line | 

{% sample lang="http" %}
**Usage**

```bash
curl -v "https://insight.io/api/project/github.com/apache/hadoop/metadata/references/trunk/org.apache.hadoop.hdfs.SWebHdfsDtFetcher.getServiceName()"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "references": {
    "10": [
      {
        "project_info": {
          "id": "github.com/apache/hadoop",
          "name": "hadoop",
          "remote_url": "https://github.com/apache/hadoop",
          "branch": "trunk",
          ...
        },
        "references": [
          {
            "file_loc": {
              "project_id": "github.com/apache/hadoop",
              "path": "hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/HdfsDtFetcher.java",
              "scm_version": "6460df21a09a7fcc29eceb8dc3859d6298da6882"
            },
            "references": [
              {
                "lineno": 51,
                "content": "  public Text getServiceName() {\n",
                "ranges": [
                  {
                    "start_offset": 14,
                    "end_offset": 28
                  }
                ]
              }
            ]
          },
          {
            "file_loc": {
              "project_id": "github.com/apache/hadoop",
              "path": "hadoop-common-project/hadoop-common/src/main/java/org/apache/hadoop/security/token/DtFetcher.java",
              "scm_version": "6460df21a09a7fcc29eceb8dc3859d6298da6882"
            },
            "references": [
              {
                "lineno": 31,
                "content": "  Text getServiceName();\n",
                "ranges": [
                  {
                    "start_offset": 7,
                    "end_offset": 21
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  }
}
```

{% endmethod %}