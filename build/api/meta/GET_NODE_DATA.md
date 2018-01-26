## Get Node Data

### Resolve Node By ID

{% method %}

This API return the details of a `Node` given its id.

```
GET /api/metadata/node/<signature>?project=<current project>&revision=<current revision>
```

`signature` is the id of the node.

| param | description |
|:-:|---|
| `project` | (Optional) restrict the node resolving to this project |
| `revision` | (Optional) restrict the node resolving to this revision |

In a successfully result, it should return a `Node`. Refer to [Meta Data](./INDEX.md) for the
explanation of the `Node` structure.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/metadata/node/org.apache.hadoop.hdfs.SWebHdfsDtFetcher"
```
{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "signature": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
  "file_loc": {
    "project_id": "github.com/apache/hadoop",
    "path": "hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/SWebHdfsDtFetcher.java",
    "scm_version": "6460df21a09a7fcc29eceb8dc3859d6298da6882"
  },
  "kind": 2,
  "lang": 0,
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
  "identifier": "SWebHdfsDtFetcher",
  "qname": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
  "content": "public class SWebHdfsDtFetcher extends HdfsDtFetcher {\n",
  "display": "SWebHdfsDtFetcher",
  "doc": "  DtFetcher for SWebHdfsFileSystem using the base class HdfsDtFetcher impl.\n"
}
```


{% endmethod %}


### Resolve Nodes By Edge

{% method %}
This API can resolve multiple `Node`s by a given `Edge`. The id (signature) of a `Node` is not necessarily unique. For
exmaple, in Apache Hadoop project, there could be a class named `org.apache.hadoop.hdfs.SWebHdfsDtFetcher`. However, you can
always create your own Java project and define a new class `org.apache.hadoop.hdfs.SWebHdfsDtFetcher` with the same package
and name. In this case, this API will return all `Node`s matching the `end_id` or `accesschain_id` of the given `Edge`.

```
GET /api/metadata/nodes?edge=<edge>
```

`edge` is the string of a full `Edge` structure after `encodeURIComponent()`.

A successful response is an array of `Node`s.

{% sample lang="http" %}
**Usage**

For a given `Edge` with `end_id` `java.lang.reflect.Array`:

```json
{
  "start_id":"mhk80lam2V9_UJEX_TGNvw__:822-827",
  "end_id":"java.lang.reflect.Array",
  "kind":0,
  "file_loc":{
    "project_id":"github.com/wyouflf/xUtils",
    "path":"library/src/com/lidroid/xutils/db/sqlite/WhereBuilder.java",
    "scm_version":"ab2bf8731c335344725952be7bfa514bdd4a047b"
  }
}
```

Curate the url as below:

```bash
$ curl -v "https://insight.io/api/metadata/nodes?edge=%7B%22start_id%22%3A%22mhk80lam2V9_UJEX_TGNvw__%3A822-827%22%2C%22end_id%22%3A%22java.lang.reflect.Array%22%2C%22kind%22%3A0%2C%22file_loc%22%3A%7B%22project_id%22%3A%22github.com%2Fwyouflf%2FxUtils%22%2C%22path%22%3A%22library%2Fsrc%2Fcom%2Flidroid%2Fxutils%2Fdb%2Fsqlite%2FWhereBuilder.java%22%2C%22scm_version%22%3A%22ab2bf8731c335344725952be7bfa514bdd4a047b%22%7D%7D"
```

{% common %}
**Response**

We find the definition of `java.lang.reflect.Array` in both JDK 7 and JDK 8.

```json
HTTP/1.1 200 OK
[
  {
    "signature": "java.lang.reflect.Array",
    "file_loc": {
      "project_id": "github.com/lambdalab-mirror/jdk8u-jdk",
      "path": "src/share/classes/java/lang/reflect/Array.java",
      "scm_version": "1cf912ef0ee695023b2e182e745335f70403ff44"
    },
    "kind": 2,
    "lang": 0,
    "range": {
      "start_loc": {
        "line": 38,
        "column": 6,
        "offset": 1581
      },
      "end_loc": {
        "line": 38,
        "column": 11,
        "offset": 1586
      }
    },
    "identifier": "Array",
    "qname": "java.lang.reflect.Array",
    "content": "class Array {\n",
    "display": "Array",
    "doc": " The {@code Array} class provides static methods to dynamically create and\n access Java arrays.\n\n <p>{@code Array} permits widening conversions to occur during a get or set\n operation, but throws an {@code IllegalArgumentException} if a narrowing\n conversion would occur.\n\n @author Nakul Saraiya\n"
  },
  {
    "signature": "java.lang.reflect.Array",
    "file_loc": {
      "project_id": "github.com/lambdalab-mirror/jdk7u-jdk",
      "path": "src/share/classes/java/lang/reflect/Array.java",
      "scm_version": "28f765b63f6151308a79500e24bf805fd01b750b"
    },
    "kind": 2,
    "lang": 0,
    "range": {
      "start_loc": {
        "line": 38,
        "column": 6,
        "offset": 1581
      },
      "end_loc": {
        "line": 38,
        "column": 11,
        "offset": 1586
      }
    },
    "identifier": "Array",
    "qname": "java.lang.reflect.Array",
    "content": "class Array {\n",
    "display": "Array",
    "doc": " The {@code Array} class provides static methods to dynamically create and\n access Java arrays.\n\n <p>{@code Array} permits widening conversions to occur during a get or set\n operation, but throws an {@code IllegalArgumentException} if a narrowing\n conversion would occur.\n\n @author Nakul Saraiya\n"
  }
]
```


{% endmethod %}


### Resolve Node

{% method %}
Sometimes, you just want to find a quick answer regarding the Node. Then `resolveNode` API just returns at most one
single `Node`. 

```
GET /api/metadata/node?edge=<edge>
```

`edge` is the string of a full `Edge` structure after `encodeURIComponent()`.

A successful response is a `Node` object or empty if failed to find one.

{% sample lang="http" %}
**Usage**
Use the same `Edge` as above.
```bash
$ curl -v "https://insight.io/api/metadata/node?edge=%7B%22start_id%22%3A%22mhk80lam2V9_UJEX_TGNvw__%3A822-827%22%2C%22end_id%22%3A%22java.lang.reflect.Array%22%2C%22kind%22%3A0%2C%22file_loc%22%3A%7B%22project_id%22%3A%22github.com%2Fwyouflf%2FxUtils%22%2C%22path%22%3A%22library%2Fsrc%2Fcom%2Flidroid%2Fxutils%2Fdb%2Fsqlite%2FWhereBuilder.java%22%2C%22scm_version%22%3A%22ab2bf8731c335344725952be7bfa514bdd4a047b%22%7D%7D"
```

{% common %}
**Response**

We find one definition of `java.lang.reflect.Array` in JDK 8.

```json
HTTP/1.1 200 OK
{
  "signature": "java.lang.reflect.Array",
  "file_loc": {
    "project_id": "github.com/lambdalab-mirror/jdk8u-jdk",
    "path": "src/share/classes/java/lang/reflect/Array.java",
    "scm_version": "1cf912ef0ee695023b2e182e745335f70403ff44"
  },
  "kind": 2,
  "lang": 0,
  "range": {
    "start_loc": {
      "line": 38,
      "column": 6,
      "offset": 1581
    },
    "end_loc": {
      "line": 38,
      "column": 11,
      "offset": 1586
    }
  },
  "identifier": "Array",
  "qname": "java.lang.reflect.Array",
  "content": "class Array {\n",
  "display": "Array",
  "doc": " The {@code Array} class provides static methods to dynamically create and\n access Java arrays.\n\n <p>{@code Array} permits widening conversions to occur during a get or set\n operation, but throws an {@code IllegalArgumentException} if a narrowing\n conversion would occur.\n\n @author Nakul Saraiya\n"
}
```

{% endmethod %}


### Resolve Node Url

{% method %}
This API can directly return a `Redirect` response, which leads you to the exact position where a
node is located, just by its id.

```
GET /api/metadata/node/redirection/<signature>?project=<current project>&revision=<current reivision>
```

`signature` is the id of the node your wish to go.

| param | description |
|:-:|---|
| `project` | (Optional) restrict the node resolving to this project |
| `revision` | (Optional) restrict the node resolving to this revision |

And the in the response header, its `Location` is set to the right location of the node on Insight.io.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/metadata/node/redirection/org.apache.hadoop.hdfs.SWebHdfsDtFetcher"
```

{% common %}
**Response**

```http
HTTP/1.1 301 Moved Permanently
Location: /github.com/apache/hadoop/trunk/hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/SWebHdfsDtFetcher.java?line=30
Content-Length: 0
Connection: keep-alive
```


{% endmethod %}