## Configurate Project

For each project on Insight.io, we expose some configuration items so that you can control the
analysis pipeline's behavior.

### Update Configurations

{% method %}

To update the configuration of a project, `POST` the configuration object.

```
POST /api/project/<project id>/config
```

`project id` is the ID of the project.

The body of this `POST` request supports the following fields

| field | description |
|:-:|---|
|`checkout`| The command lines to be executed before checking out the project. |
|`dependencies`| The command lines to be executed before resolving the dependencies of the project. |
|`build`|  The command lines to be executed before building the project. |
|`general`|  The command lines to be executed after all the build analysis finished. |
|`branch` | The main analysis branch. |
|`manualUpdate | If the project should only update manually through [Update Project](../administration/UPDATE_PROJECT.md). By default, the system periodically updates the repository. |

{% sample lang="http" %}
**Usage**
```bash
$ curl -v \
  -H "Content-Type: application/json" \
  -d '{"checkout":"mkdir build", "branch":"master", "manualUpdate":true}' \
  https://insight.io/api/project/github.com/apache/commons-logging/config?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 202 Accepted
```

{% endmethod %}


### Get Configurations

{% method %}

This `GET` API returns the current configuration of a given project.

```
GET /api/project/<project id>/config
```

`project id` is the ID of the project.

A successful response is the configuration object which has all the fields above, but also `allBranches`, which is an array of all the available branches of this project.

{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/project/github.com/apache/commons-logging/config?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "checkout": "mkdir build",
  "dependencies": "",
  "build": "",
  "branch": "master",
  "general": "",
  "manualUpdate": true,
  "allBranches": [
    "trunk",
    "DON_QUIXOTE",
    "RELEASE_BRANCH_1_0_5",
    "REVISED_DISCOVERY",
    "allow-flawed",
    "simon-1.1"
  ],
  "projectId": "github.com/apache/commons-logging"
}
```

{% endmethod %}