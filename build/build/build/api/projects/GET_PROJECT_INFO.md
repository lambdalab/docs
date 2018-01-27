## Get Project Information

{% method %}
This API returns all the meta information regarding a project, e.g. clone url, its internal 
status, etc., as known as `ProjectInfo`. `ProjectInfo` serves as the orthodox representation
of a project in Insight.io.

```
GET /api/project/<project id>/info
```

For a public project, you don't need to provide anything to get the result. For a private
project, however, you have to provide an access token for authorization.

A successful response is a `ProjectInfo` object, which contains the following fields:

| field | description |
|:-:|---|
|`name`| the name of this project |
|`remote_url`| the git clone url of this project |
|`branch`| the main branch of this project |
|`main_branch`| the specified analysis branch of this project |
|`description`| the description of this project |
|`language`| the major programming language of this project (inhertied from Github) |
|`owner`| the name of the owner/organization of this project |
|`is_private`| if this project is a private project |
|`enable_manual_update`| if this project is only allowed to update manually |
|`clone_status`| the status of the clone stage of the analysis pipeline towards this project |
|`color_status`| the status of the syntax coloring stage of the analysis pipeline towards this project |
|`index_status`| the status of the elastic search indexing stage of the analysis pipeline towards this project |
|`build_status`| the current serving status of the static analysis stage of the analysis pipeline towards this project |
|`build_status_list`| A list of static analysis status for multiple revisions. Normally this has one item. It could have 2 items when the project is in build after update. One for the revision for serving Metadata. The other for the revision in build. |

Each of the status is a `ProjectState` object, which has the following fields:

| field | description |
|:-:|---|
|`revision`| the revision of the project in analysis pipeline |
|`state`| the state of this stage |
|`timestamp`| the timestamp of the moment when this status is recently updated |
|`revision_timestamp`| (Optional) the timestamp when this change is committed by the author |
|`branch`| (Optional) the branch of this revision |

Each `state` is an enumeration with the following values:

| value | description |
|:-:|-----|
|`0`| INIT |
|`1`| ONGOING |
|`2`| FINISHED |
|`3`| FAILED |
|`100`| UNKNOWN |


{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/project/github.com/apache/commons-logging/info
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "name": "commons-logging",
  "remote_url": "https://github.com/apache/commons-logging",
  "branch": "trunk",
  "clone_status": {
    "revision": "3e3b8446a76b4a9016c6a9a2343a494a9d98579b",
    "state": 2,
    "timestamp": 1498264799859
  },
  "index_status": {
    "revision": "3e3b8446a76b4a9016c6a9a2343a494a9d98579b",
    "state": 2,
    "timestamp": 1498264919621
  },
  "color_status": {
    "revision": "3e3b8446a76b4a9016c6a9a2343a494a9d98579b",
    "state": 2,
    "timestamp": 1498264807770
  },
  "build_status": {
    "revision": "3e3b8446a76b4a9016c6a9a2343a494a9d98579b",
    "state": 2,
    "timestamp": 1498264878582,
    "revision_timestamp": 1496499350,
    "branch": "trunk"
  },
  "build_status_list": [
    {
      "revision": "3e3b8446a76b4a9016c6a9a2343a494a9d98579b",
      "state": 2,
      "timestamp": 1498264878582,
      "revision_timestamp": 1496499350,
      "branch": "trunk"
    }
  ],
  "description": "Mirror of Apache Commons Logging",
  "language": "Java",
  "owner": "apache",
  "is_private": false,
  "enable_manual_update": false
}
```

{% endmethod %}