## Get Commit Diff View

{% method %}

This API could get the exact change of a file in a particular commit. So by
following up the result of [Get A Single Commit](./GET_COMMITS.md) and using this API, you can create the full view of a commit.

```
GET /api/project/<project id>/diffView/<revision>/<filepath>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `revision` | the revision of the commit |
| `filepath` | the target filepath of the diff |

In a successful response, the `diff` field contains the complete details to
render a full change of the given file.

| field | description |
|:-:|---|
| `diff_type` | The type of the change on this file |
| `new_path` | The new path of the file |
| `old_path` | The old path of the file |
| `new_content` | The full content of the file after change |
| `old_content` | The full content of the file before change |
| `new_content_format` | The syntax formats of the file after change |
| `old_content_format` | The syntax formats of the file before change |
| `edit_list` | An array of edits of this diff |

Regarding the `content` and `status` fields in `new_content`/`old_content` and the structure of `content_format` fields, you can find them in [Get File Content](./GET_FILE_CONTENT.md).

The `diff_type` is an enumeration, which includes the following possible values:

| value | description |
|:-:|---|
| `0` | this file is added |
| `1` | this file is modified |
| `2` | this file is deleted |
| `3` | this file is renamed |
| `4` | this file is copied |

The `edit_list` structure defines the entire change of this diff. For each edit, it has
the following fields:

| field | description |
|:-:|---|
| `edit_type` | the type of this field. See below for more details of this enumeration. |
| `begin_a` | the edit's start offset in the whole file on the left side. |
| `end_a` | the edit's end offset in the whole file on the left side. |
| `begin_b` | the edit's start offset in the whole file on the right side. |
| `end_b` | the edit's end offset in the whole file of the right side. |
| `begin_line_a` | the edit's start line on the left side. |
| `end_line_a` | the edit's end line on the left side. |
| `begin_line_b` | the edit's start line on the right side. |
| `end_line_b` | the edit's end line on the right side. |

The `edit_type` is an enumeration, which has the following values:

| value | description |
|:-:|---|
| `0` | Insert |
| `1` | Delete |
| `2` | Replace |
| `3` | Empty |


{% sample lang="http" %}
**Usage**

```bash
curl -v "https://insight.io/api/project/github.com/apache/hadoop/diffView/f214a996/hadoop-tools/hadoop-aws/src/test/java/org/apache/hadoop/fs/s3native/NativeS3FileSystemContractBaseTest.java"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "diff": {
    "diff_type": 1,
    "new_path": "hadoop-tools/hadoop-aws/src/test/java/org/apache/hadoop/fs/s3native/NativeS3FileSystemContractBaseTest.java",
    "old_path": "hadoop-tools/hadoop-aws/src/test/java/org/apache/hadoop/fs/s3native/NativeS3FileSystemContractBaseTest.java",
    "new_content": {
      "content": "<new file content>",
      "status": 0
    },
    "old_content": {
      "content": "<old file content>",
      "status": 0
	},
	"edit_list": [
      {
        "edit_type": 1,
        "begin_a": 1765,
        "end_a": 1845,
        "begin_b": 1765,
        "end_b": 1765,
        "begin_line_a": 46,
        "end_line_a": 48,
        "begin_line_b": 46,
        "end_line_b": 46
      },
      {
        "edit_type": 0,
        "begin_a": 2030,
        "end_a": 2030,
        "begin_b": 1950,
        "end_b": 2030,
        "begin_line_a": 53,
        "end_line_a": 53,
        "begin_line_b": 51,
        "end_line_b": 53
      },
      {
        "edit_type": 2,
        "begin_a": 2135,
        "end_a": 2160,
        "begin_b": 2135,
        "end_b": 2193,
        "begin_line_a": 58,
        "end_line_a": 59,
        "begin_line_b": 58,
        "end_line_b": 61
      }
    ],
    "new_content_format": [
	  [
	    [0, 3, "cm"]
	  ],
	  [
	    [0, 61, "cm"]
	  ]
	],
    "old_content_format": [
	  [
	    [0, 3, "cm"]
	  ],
	  [
	    [0, 61, "cm"]
	  ]
	]
  }
}
```



{% endmethod %}