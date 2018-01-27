# Git Data

Git data related APIs provide you the access to read the git repository
served on Insight.io. Since Insight.io current acts as a source code
browsing service, instead of code hosting, we currently provide a subset
of all available git operations.

In the meantime, we wrap the raw git operations based on our own needs so
that these APIs could return structured data for versatile usages.

For public repository, you don't need to provide any credentials for all
these APIs. However, if it's an private repo, make sure you do have the correct permission to get the correct response. Refer to [Authentication](../authentication/INDEX.md) to know more about access control.

This chapter has the following sections:

* [Get File Content](./GET_FILE_CONTENT.md)
* [Get File List](./GET_FILE_LIST.md)
* [Get Branches](./GET_BRANCHES.md)
* [Get Tags](./GET_TAGS.md)
* [Get Commits](./GET_COMMITS.md)
* [Get Commit Diff](./GET_COMMIT_DIFF_VIEW.md)
* [Get Blames](./GET_BLAMES.md)
