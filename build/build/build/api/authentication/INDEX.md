# Authentication

Insight.io has a robust user permission system equipped. For APIs, the permission 
system also applies. To correct retrieve your desired data and execute the right
operation towards Insight.io, you have to understand how to verify your identity
through this permission system, and the very first step for any APIs usages is go through our authentication process.

In this chapter, you will learn the concept of **API Access Token** and the way
to manage and use them.

## Api Access Token

Api access token acts like ordinary OAuth token, so that you don't need to bear the password and username with you  all the time. You can understand it as a counterpart of [Personal Access Tokens](https://github.com/settings/tokens) of Github. On Insight.io, api access token is not only enabled for username/password authentication, but also for all other supported third party OAuth services enabled. This documentation shows you have to leverage api access token to interact with Insight.io with more flexibility.

An user could create as many api access token as he/she wants, but be extremely careful that whenever a token is created, it works forever until you revoke it explicitly. So we highly recommend to always actively manage your api access tokens whenever necessary.

This chapter has the following sections:

* [Token Creation](./TOKEN_CREATION.md)
* [Get All Tokens](./TOKEN_LIST.md)
* [Revoke a Token](./TOKEN_REVOKE.md)
* [Token Usage](./TOKEN_USAGE.md)
* [Manage Token on UI](./TOKEN_MANAGEMENT_UI.md)