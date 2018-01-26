# Projects

To call these project related APIs, you have to provide your identity along with your API call.
Go to [Authentication](./authentication/INDEX.md) section to know more about the [API Access Token Usage](./authentication/TOKEN_USAGE.md). Without the correct token, you will get a response message:

```json
{
  "error":"Credentials required"
}
```

A couple of concepts to keep in mind before go ahead:

* `project id`: This acts as the ID of any project on Insight.io, its constructed by joining
the `domain`, `organization` and `name` together with `/`, following this pattern:
`<domain>/<organization>/<name>`. For example, `github.com/apache/hadoop` is the ID of
[Apache Hadoop](https://github.com/apache/hadoop), where `domain` is `github.com,
`organization` is `apache` and `name` is `hadoop`.

This chapter has the following sections:

* [Get Project Detailed Information](./GET_PROJECT_INFO.md)
* [Get All Projects in System](./GET_ALL_PROJECTS.md)
* [Get All Projects of User](./GET_USER_PROJECTS.md)
* [Get Recent Viewd Projects](./GET_RECENT_PROJECTS.md)
* [Get Starred Projects](./GET_STARRED_PROJECTS.md)
* [Get Project Analysis Log](./GET_PROJECT_ANALYSIS_LOG.md)