# Switch a Repo from Public to Private

If you want to switch an already imported public repo to private, you can do so by calling the following API:

```
POST /api/switchRepoToPrivate/<projectId>
```

Note that this API requires admin priviledge to call.

After a repo is switched to private, only admin has access to it by default, you may need to push access setting for the private repo to control how it can be accessed by other users.
