## Get Full Text Search Data

{% method %}
This API returns the full search data `GET /api/search/federated`. You have to provide the following params in the url.

* `q`: Required. The query string, e.g. "config"
* `projid`: Required. The project id the query is limited to, if project id is empty string "", the search will be across all projects
* `searchType`: Required. Specify the type of result, either 'code' or 'project'
* `l`: Optional. Specify the language of result, has to be one of "java", "scala", "cpp", "python", "ruby", "xml", "html", "shell", "txt", "php", "unknown"
* `page`: Optional. The page of the result



A valid response contains an array of nodes, with each node having the following data structure:

| field | description |
|:-:|---|
|`term`| the queried language |
|`total`| total results avaiable |
|`page`| the page of the current results |
|`result`| the list of search results|
|`facet`| the facet of search results|

Each search result contains the following field:

| field | description |
|:-:|---|
|`range`| the range of the current result, range is a pair of (start, end) tuples that marks the start and end position of the snippet |
|`content`| the content surrounding the search result |
|`hightlight`| the hightlight information of the snippet, a list of range where the snippet should be highlighted |
|`pathhighlight`| the hightlight information for the path, a list of range where the path should be highlighted|
|`color`| the coloring each line of the snippet|
|`path`| the path of the result|
|`projectId`| the project Id of the project the search result belongs to|
|`projectOwner`| the owner of the project|
|`projectName`| the name of the project|
|`branch`| the branch the search result belongs to|

Each facet contains the a list of the following field:

|`facetName`| the name of facet|
|`terms`| the list of terms under the facet, a term is a tuple of term and count|




{% sample lang="http" %}
**Usage**
```bash
$ curl -v "api/federatedSearchResult?q=hadoop&searchType=code&page=1&projid=github.com%2Fapache%2Fhadoop&l=java"
```


{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "term": [
    "java"
  ],
  "total": 8055,
  "page": 1,
  "perPage": 15,
  "result": [
    {
      "range": [
        {
          "start": 18,
          "end": 18
        },
        {
          "start": 26,
          "end": 42
        }
      ],
      "score": 22.49978256225586,
      "content": "\npackage org.apache.hadoop.lib.service.hadoop;\n\n\nimport org.apache.hadoop.conf.Configuration;\nimport org.apache.hadoop.fs.CommonConfigurationKeysPublic;\nimport org.apache.hadoop.fs.FileSystem;\nimport org.apache.hadoop.fs.Path;\nimport org.apache.hadoop.lib.server.Server;\nimport org.apache.hadoop.lib.server.ServiceException;\nimport org.apache.hadoop.lib.service.FileSystemAccess;\nimport org.apache.hadoop.lib.service.FileSystemAccessException;\nimport org.apache.hadoop.lib.service.instrumentation.InstrumentationService;\nimport org.apache.hadoop.lib.service.scheduler.SchedulerService;\nimport org.apache.hadoop.test.HFSTestCase;\nimport org.apache.hadoop.test.TestDir;\nimport org.apache.hadoop.test.TestDirHelper;\nimport org.apache.hadoop.test.TestException;\nimport org.apache.hadoop.test.TestHdfs;\nimport org.apache.hadoop.test.TestHdfsHelper;\nimport org.apache.hadoop.util.StringUtils;",
      "highlight": [
        {
          "range": {
            "start_loc": {
              "line": 18,
              "column": 19,
              "offset": 827
            },
            "end_loc": {
              "line": 18,
              "column": 25,
              "offset": 833
            }
          },
          "score": 0,
          "term": "hadoop"
        },
        {
          "range": {
            "start_loc": {
              "line": 27,
              "column": 18,
              "offset": 1055
            },
            "end_loc": {
              "line": 27,
              "column": 24,
              "offset": 1061
            }
          },
          "score": 0,
          "term": "hadoop"
        }
      ],
      "totalHits": 54,
      "color": [
        [],
        [
          [
            0,
            7,
            "kn"
          ],
          [
            8,
            36,
            "nn"
          ]
        ]
      ],
      "pathhiglight": [
        {
          "range": {
            "start_loc": {
              "line": 0,
              "column": 0,
              "offset": 0
            },
            "end_loc": {
              "line": 0,
              "column": 6,
              "offset": 6
            }
          },
          "score": 0,
          "term": "hadoop"
        }
      ],
      "path": "hadoop-hdfs-project/hadoop-hdfs-httpfs/src/test/java/org/apache/hadoop/lib/service/hadoop/TestFileSystemAccessService.java",
      "projectId": "github.com/apache/hadoop",
      "projectOwner": "apache",
      "projectName": "hadoop",
      "branch": "trunk"
    }
  ],
  "facet": [
    {
      "facetName": "Languages",
      "terms": [
        {
          "term": "Java",
          "count": 8055
        },
        {
          "term": "Unknown",
          "count": 708
        },
        {
          "term": "Xml",
          "count": 215
        },
        {
          "term": "Shell",
          "count": 41
        },
        {
          "term": "Html",
          "count": 39
        },
        {
          "term": "Txt",
          "count": 24
        },
        {
          "term": "Python",
          "count": 3
        },
        {
          "term": "Javascript",
          "count": 3
        }
      ]
    }]
}
```


{% endmethod %}