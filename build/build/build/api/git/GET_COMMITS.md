## Get Commits


### Get Multiple Commits
{% method %}

This API could retrieve a consequtive of commit at a time.

```
GET /api/project/<project id>/commits/<path>?startRevision=<revision>&start=<start>&end=<end>
```

| param | description |
|:-:|---|
| `project id` | the id of the project |
| `startRevision` | the start revision |
| `start` | the related distance of the commit before the given revision and the given commit of the given revision. Serves as the begin of the range. |
| `end` | the related distance of the commit before the given revision and the given commit of the given revision. Serves as the end of the range. |
| `path` | the path that all the commits should affects. (Optionsal) If not provided, use `root` path |

In a successful response, the `commits` field contains all the commits.
Each commit has the following fields:

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

This example gets the most recent 20 commits under `/hadoop-tools` in `trunk` branch of hadoop project.

```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/commits/hadoop-tools/?startRevision=trunk&start=0&end=20"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "commits": [
    {
      "sha": "dd65eea74b1f9dde858ff34df8111e5340115511",
      "hashcode": 73997436,
      "email": "jlowe@yahoo-inc.com",
      "timestamp": 1497970427000,
      "name": "Jason Lowe",
      "short_message": "HADOOP-8143. Change distcp to have -pb on by default. Contributed by Mithun Radhakrishnan",
      "parent_revisions": [
        "3369540653a41dd0194b65f5ef1d53225fb97ba8"
      ]
    },
    {
      "sha": "3369540653a41dd0194b65f5ef1d53225fb97ba8",
      "hashcode": 1796417937,
      "email": "aajisaka@apache.org",
      "timestamp": 1497932306000,
      "name": "Akira Ajisaka",
      "short_message": "HADOOP-14296. Move logging APIs over to slf4j in hadoop-tools.",
      "parent_revisions": [
        "f214a9961fdeeebc6157992ed54a777983e218e9"
      ]
    },

    ...

    {
      "sha": "f214a9961fdeeebc6157992ed54a777983e218e9",
      "hashcode": -472405398,
      "email": "liuml07@apache.org",
      "timestamp": 1497550576000,
      "name": "Mingliang Liu",
      "short_message": "HADOOP-14494. ITestJets3tNativeS3FileSystemContract tests NPEs in teardown if store undefined. Contributed by Steve Loughran",
      "parent_revisions": [
        "325163f23f727e82379d4a385b73aa3a04a510f6"
      ]
    },
  ]
}
```


{% endmethod %}


### Get A Single Commit
{% method %}

To get the details of a single commit, you can

```
GET /api/project/<project id>/commit/<revision>
```


| param | description |
|:-:|---|
| `project id` | the id of the project. |
| `revision` | the revision of the commit. this could be either a SHA or a reference name (branch/tag). |

The details is included in the `commit` field, which has the following fields:

| field | description |
|:-:|---|
| `sha` | The SHA number of this commit |
| `hashcode` | The hash code of this commit |
| `email` | The email of the author |
| `timestamp` | The timestamp when this commit is created |
| `name` | The name of the author |
| `short_message` | The message of the commit |
| `full_message` | The full message of the commit |
| `parent_revisions` | The revisions of the parent commits of this commit. |
| `files` | The array of touched files of the commit. |

Each element of the `files` has the summary of midifications of the file:

| field | description |
|:-:|---|
| `new_path` | The new path of the file |
| `old_path` | The old path of the file |
| `diff_type` | The type of the change |
| `add_lines` | The number of lines added |
| `delete_lines` | The number of lines removed |

The `diff_type` is an enumeration, which includes the following possible values:

| field | description |
|:-:|---|
| `0` | this file is added |
| `1` | this file is modified |
| `2` | this file is deleted |
| `3` | this file is renamed |
| `4` | this file is copied |


{% sample lang="http" %}
**Usage**

```bash
$ curl -v "https://insight.io/api/project/github.com/apache/hadoop/commit/f214a996"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
{
  "commit": {
    "sha": "f214a9961fdeeebc6157992ed54a777983e218e9",
    "hashcode": -472405398,
    "email": "liuml07@apache.org",
    "timestamp": 1497550576000,
    "name": "Mingliang Liu",
    "short_message": "HADOOP-14494. ITestJets3tNativeS3FileSystemContract tests NPEs in teardown if store undefined. Contributed by Steve Loughran",
    "full_message": "HADOOP-14494. ITestJets3tNativeS3FileSystemContract tests NPEs in teardown if store undefined. Contributed by Steve Loughran\n",
    "parent_revisions": [
      "3f5108723c6272d2fded8d3563c4b793e1d88f8b"
    ],
    "files": [
      {
        "new_path": "hadoop-tools/hadoop-aws/src/test/java/org/apache/hadoop/fs/s3native/NativeS3FileSystemContractBaseTest.java",
        "old_path": "hadoop-tools/hadoop-aws/src/test/java/org/apache/hadoop/fs/s3native/NativeS3FileSystemContractBaseTest.java",
        "diff_type": 1,
        "add_lines": 5,
        "delete_lines": 3
      }
    ]
  }
}
```


{% endmethod %}