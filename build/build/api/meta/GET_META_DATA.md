## Get Meta Data

{% method %}

The API can load all the meta data required to build the full context of a given source file.

```
GET /api/project/<project id>/metadata/<revision>/<filepath>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `revision` | the revision of the project |
| `filepath` | the file path of all the meta data your wish to load |

In a successful response, it has the following fields:

| field | description |
|:-:|-----|
| `file_loc` | The location of the requested file |
| `nodes` | All the nodes included in this source file |
| `edges` | All the edges with start node included in this source file |
| `lang` | The programming language of this source file |

The `lang` field is an enumeration, which has the following values:

| value | description |
|:-:|-----|
|`0`| Java |
|`1`| Scala |
|`2`| C++ |
|`3`| Python |
|`4`| Javascript |
|`5`| Ruby |
|`6`| XML |
|`7`| Html |
|`8`| Shell |
|`9`| Txt |
|`10`| Php |
|`100`| Unknown |

For the explanation of `Node` and `Edge`, refer to [Meta Data](./INDEX.md).

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/metadata/trunk/hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/SWebHdfsDtFetcher.java"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "file_loc": {
    "project_id": "github.com/apache/hadoop",
    "path": "hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/SWebHdfsDtFetcher.java",
    "scm_version": "6d116ffad23b470f8e9ca131d8e89cbbbb4378d7"
  },
  "nodes": [
    {
      "signature": "0X_8smfRb28NmAqJiuyAeA__",
      "kind": 1,
      "range": {
        "start_loc": {
          "line": 0,
          "column": 0,
          "offset": 0
        },
        "end_loc": {
          "line": 0,
          "column": 0,
          "offset": 0
        }
      }
    },
    {
      "signature": "0X_8smfRb28NmAqJiuyAeA__:875-878",
      "kind": 9,
      "range": {
        "start_loc": {
          "line": 20,
          "column": 34,
          "offset": 875
        },
        "end_loc": {
          "line": 20,
          "column": 37,
          "offset": 878
        }
      }
    },
    
    ...

    {
      "signature": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
      "kind": 2,
      "range": {
        "start_loc": {
          "line": 29,
          "column": 13,
          "offset": 1113
        },
        "end_loc": {
          "line": 29,
          "column": 30,
          "offset": 1130
        }
      },
      "qname": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
      "display": "SWebHdfsDtFetcher",
      "doc": "  DtFetcher for SWebHdfsFileSystem using the base class HdfsDtFetcher impl.\n"
    },
    {
      "signature": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher.getServiceName()",
      "kind": 7,
      "range": {
        "start_loc": {
          "line": 35,
          "column": 14,
          "offset": 1339
        },
        "end_loc": {
          "line": 35,
          "column": 28,
          "offset": 1353
        }
      },
      "qname": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher.getServiceName",
      "display": "getServiceName(): Text"
    }
  ],
  "edges": [
    {
      "start_id": "0X_8smfRb28NmAqJiuyAeA__",
      "end_id": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
      "kind": 6
    },
    {
      "start_id": "0X_8smfRb28NmAqJiuyAeA__:1007-1011",
      "end_id": "org.apache.hadoop.io.Text",
      "kind": 0
    },

    ...

    {
      "start_id": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
      "end_id": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher.getServiceName()",
      "kind": 6
    }
  ],
  "lang": 0
}
```

{% endmethod %}