# User

To call these user related APIs, you have to provide your identity along with your API call. Go to 
[Authentication](./authentication/INDEX.md) section to know more about the [API Access Token Usage](./authentication/TOKEN_USAGE.md). Without the correct token, you will get a response message:

```json
{
  "error":"Credentials required"
}
```

This chapter has the following sections:

* [Get User Profile](./user/GET_USER_PROFILE.md)
* [Get Linked Services](./user/GET_LINKED_SERVICES.md)
* [Manage Starred Files](./user/STAR_FILES.md)
* [Manage Recent Visited Files](./user/RECENT_FILES.md)
* [Manage Imported Projects](./user/MANAGE_IMPORTED_PROJECTS.md)