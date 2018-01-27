# Administration

Only the administrator of the system would have the permission to call administration APIs. On Insight.io, the first
registered user automatcially acquire the administrator's role. Later, the administrator can grant administration
permission to other users.

To call these administration APIs, you have to provide your identity along with your API call. Go to 
[Authentication](./authentication/INDEX.md) section to know more about the [API Access Token Usage](./authentication/TOKEN_USAGE.md). Without the correct token, you will get a response message:

```json
{
  "error":"Credentials required"
}
```

This chapter has the following sections:

* [Create Project](./administration/CREATE_PROJECT.md)
* [Find A Project](./administration/FIND_PROJECT.md)
* [Update A Project](./administration/UPDATE_PROJECT.md)
* [Re-Analyze A Project](./administration/REANALYZE_RPOJECT.md)
* [Remove A Project](./administration/REMOVE_PROJECT.md)
* [Config Project Analysis](./administration/CONFIG_PROJECT_ANALYSIS.md)
* [Get All Users](./administration/GET_ALL_USERS.md)
* [Add An Admin User](./administration/ADD_ADMIN_USER.md)
* [Remove An Admin User](./administration/REMOVE_ADMIN_USER.md)
