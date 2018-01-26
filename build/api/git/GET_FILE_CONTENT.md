## Get File Content

{% method %}
To get the content of any file in the git repository, you can access `GET /api/loadFilePrimaryData`. You have to provide the following params in the url.

* `project id`: The id of the git repository. Normally, it looks like
`github.com/apache/hadoop` in Insight.io.
* `revision`: the revision of the file
* `filepath`: the path of the file in the given revision


```
GET /api/project/<project id>/fileContent/<revision>/<filepath>
```

A valid response contains the following fields

| field | description |
|:-:|---|
|`content`| The content of the file you requested. |
|`status`| The status of the file, see next section for more details. |
|`format`| the syntax highlights array of the file content. |
|`title`| the title of this file |
|`description`| the description of this file |

This `format` array is a 3 dimentional array. The top level array's length is the same as the number
of lines in the `content`. Each element contains an array of syntax highligts
of this particular line. For each syntax highlight, it's a 3 element array. The first and second elements are the syntax highlight's offset range, and
the last element serves as the type of syntax, e.g. comment, function, variable, etc. 

{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/fileContent/trunk/hadoop-hdfs-project/hadoop-hdfs/src/main/java/org/apache/hadoop/hdfs/SWebHdfsDtFetcher.java"
```


{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "content": "...<file content>",
  "status": 0,
  "format": [
    [
      [0, 3, "cm"]
    ],
    [
      [0, 61, "cm"]
    ],
    [
      [0, 63, "cm"]
    ],
    [
      [0, 56, "cm"]
    ],
    []
    [],
    [
      [0, 52, "cm"]
    ]
  ]
  "title": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher in hadoop | Insight.io",
  "description": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher in hadoop. Insight.io provides an IDE-like code browsing experience on the web"
}
```


{% endmethod %}


### Status
{% method %}

In the example above, you have see a request with normal successfully
response. However, there are cases when the file content is **invalid**
in Insight.io's context as follows:

| status | description |
|:-:|---|
| `0` | the file content is fetched successfully. |
| `1` | the size of file content is too big (> 2MB). |
| `2` | the content of the file is not text. |
| `3` | the file does not exist. |
| `4` | unknown status. |


{% sample lang="http" %}
**Usage**
```bash
$ curl -v "https://insight.io/api/project/github.com/apache/sqoop/fileContent/trunk/lib/ant-contrib-1.0b3.jar"
```

{% common %}
**Response**
Because the requested file is a `jar` file, which is not in text format, you will get a status of `2`

```json
HTTP/1.1 200 OK
{
  "content": "",
  "status": 2,
  "format": [],
  "title": "lib/ant-contrib-1.0b3.jar in sqoop | Insight.io",
  "description": "lib/ant-contrib-1.0b3.jar in sqoop. Insight.io provides an IDE-like code browsing experience on the web"
}
```

{% endmethod %}
