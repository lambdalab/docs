# Find Project via Url


You can also check if a repo has been imported or not by using following API

```
GET /api/admin/findProject?url=$repoUrl
```

Note that `repoUrl` must be encoded as valid URL component.

This API will return a project information if the project is existed. `response.id` is the **Project ID** we used for other API access.
It will return 404 if the repo hasn't been imported.