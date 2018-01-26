## Configure manual user permission management

By default, the system try to sync permission from github / gitlab. If we need to manually manage all the permission, we need to do the following

### Disable permission sync

Add the following configuration to `user.conf`.

```
codatlas.enableManualAccessControl: true
```

### Push User Access though API

You can update access of a user by calling the following API:

```
POST /api/admin/pushUserAccess
```

Set `Content-Type` to `application/json` and `POST` with body:

```json
{
  "userId":"testuser",  // userId of the user
  "providerId":"gitlab", // providerId of the user
  "projectIds" : ["github.com/apache/sqoop", "github.com/dmlc/dmlc-core"] //projectIds of the repos the user can access
}
```

Where userId is the id that is used for login, providerId is the type of the login,
* if the user is configured to login with github, then providerId is "github",
* if the user is configured to login with ldap, then providerId should be "ldap",
* if the user is configured to login with normal username / password, then the providerId should be "userpass"

Note that this API requires admin priviledge to call, and this API only works when github or gitlab integration is not configured
for the system