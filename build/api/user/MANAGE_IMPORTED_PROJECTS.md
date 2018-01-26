## Manage Imported Projects

For users linked with other Git repository hosting services, e.g. GitLab, GitHub, they can
import projects directly into Insight.io, or delete imported projects, which has already been
imported into Insight.io.

### Import Project

{% method %}
This API will import an user project into Insight.io.

```
POST /api/user/project?url=<url>&origin=<origin>&private=<private>
```

Use the following query string to provide details of the project.

| param | description |
|:-:|---|
| `url` | the url of the project |
| `origin` | (Optional) the origin of the project |
| `private` | (Optional) if true, mark this imported project as a private project |

The `origin` currently supports GitLab (`5`) and GitHub (`1`). If not provided, then use
GitLab by default.

The system will talk to the linked service to check if the given url does belong to
current user, before import this project.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v -X POST "https://insight.io/api/user/project?url=https://github.com/abc/test&origin=1&token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

```json
HTTP/1.1 200 OK
```

{% endmethod %}

### Remove Imported Project

{% method %}

This API undos the one above and remove an imported project from the system.

```
DELETE /api/user/project/<project id>
```

If failed to find the project with `project id`, you will get a `404 Not Found`.

{% sample lang="http" %}
**Usage**

```bash
$ curl -v -X DELETE "https://insight.io/api/user/project/github.com/abc/test?token=833808b68d2ebfd8e4db5aaf59085851f756a3f0f9d528b4063f831b8fe9755a"
```

{% common %}
**Response**

If found the project and remove successfully:

```json
HTTP/1.1 200 OK
```

Otherwise,

```json
HTTP/1.1 404 Not Found
```

{% endmethod %}