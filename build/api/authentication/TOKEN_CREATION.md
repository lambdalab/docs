## Token Creation

There are 2 ways to create an api access token, either via API, or via Insight.io UI, which can be found at [Manage API Token on Insight.io](./TOKEN_MANAGEMENT_UI.md)


### Creation after Authentication

{% method %}
If you have already logged into Insight.io already, we can recognize you from your cookie. `POST /api/token` will
generate a new token and return it to you.


```
POST /api/token
```

{% sample lang="http" %}
**Usage**
```bash
$ curl -i -X POST --cookie "<your logged in cookie>" https://insight.io/api/token
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "token":"83dc9844fc388b8f3aecf1f430a3fd58b0abd9da834c19c8c906aa992fe0c279fa5da21b20665dff985ab55cd11dfb0dcc618ebc83736dfc642ee1b6fd01a001b1a3e83e4264ce9acc3318a4836d2c82e84cc82408369f298a13bd2f249b162a7bb3443947b9c41788d662c9306b36af4c3caa6dd523eec7df1685922ee55540"
}
```
{% endmethod %}

### Creation before Authentication

You can also create an api access token without manually login.
This is mostly useful for interact with Insight.io programmatically.
Depends on how do you authenticate with Insight.io, the usage also varies.

#### Username/Password

{% method %}
If you have normal username/password account, simply `POST` your username and password to `/api/authenticate/userpass`
to authenticate your account and this will generate a new access token to you.


```
POST  /api/authenticate/userpass
```

{% sample lang="http" %}
**Usage**

```bash
$ curl -i --data "username=<your username>&password=<your password>" <host>/api/authenticate/userpass
```

{% common %}
**Response**
```json
HTTP/1.1 200 OK
{
  "token":"961bb2a95e2184a97729398f39c2090b404c07d98cfda7fee6f7d1349d7c6b3577321b49ae920bb1cb4fb30862eb2d7583766a01df6680ffff0094cade160dfa04bce5e0d3fa7e2b43bd5371d1a0ab3b79bba592dbfc5f51dc75871ed4212d2549eac819a51beeaf588fb5e5d00d6241182264240f9c370e960f954a014889c0",
  "expiresOn":"292278994-08-17T07:12:55.807Z"
}
```
{% endmethod %}


#### LDAP

{% method %}

Similar to use username and password, `POST` your LDAP username and password to `/api/authenticate/ldap` instead, without
the need to register on Insight.io before.

```
POST /api/authenticate/ldap
```

{% sample lang="http" %}
**Usage**
```bash
$ curl -i --data "username=<your ldap username>&password=<your password>" <host>/api/authenticate/ldap
```
{% endmethod %}

#### OAuth

{% method %}

To create api access token with a third party OAuth service, `POST` your OAuth information to `/api/authenticate/<provider>` with the following **json** body:

```
POST /api/authenticate/<provider>
```

```json
{
	"email": "<your email address>",
	"info": {
		"accessToken": "<your OAuth token>"
	}
}
```

{% sample lang="http" %}
**Usage**

Take Github as an example:

```bash
$ curl -i --header "Content-Type: application/json" --data "{'email':'<your email>', 'info': { 'accessToken': '<your OAuth token>' }}" <host>/api/authenticate/github
```

{% common %}
**Response**

You will get response as below if authenticate successfully
```json
HTTP/1.1 200 OK
{
  "token":"961bb2a95e2184a97729398f39c2090b404c07d98cfda7fee6f7d1349d7c6b3577321b49ae920bb1cb4fb30862eb2d7583766a01df6680ffff0094cade160dfa04bce5e0d3fa7e2b43bd5371d1a0ab3b79bba592dbfc5f51dc75871ed4212d2549eac819a51beeaf588fb5e5d00d6241182264240f9c370e960f954a014889c0",
  "expiresOn":"292278994-08-17T07:12:55.807Z"
}
```
{% endmethod %}
