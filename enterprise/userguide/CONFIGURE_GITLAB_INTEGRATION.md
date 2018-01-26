# Configure Gitlab Integration

Insight.io also support integration with `Gitlab`. This section describes the operations to integrate with `Gitlab <https://gitlab.com/>`_.


**Normal Integration**

Similar to configuring github integration, the first step is to create a new OAuth application. Log into your gitlab account and go to `settings` page, then click on `Application` tag, and then enter a name for your application. The name can be any of your preferred strings. Fill the public IP/DNS of your host server into `Redirect URI` followed with `/authenticate/gitlab`, e.g. `http://ec2-52-35-135-191.us-west-2.compute.amazonaws.com/authenticate/gitlab`. Then add `api` scope and `read_user` scope. Finally, finish creating the OAuth application by clicking save application.

Go back to the bash terminal, open and edit the `user.conf` file:

```bash
vi ./lambdalab-docker/configs/user.conf
```

Add the authorization/accessToken url and the newly acquired OAUTH client ID and OAUTH client secret into the config:

```bash
gitlab {
  baseUrl="YOUR-GITLAB-URL"
  authorizationUrl=${securesocial.gitlab.baseUrl}/login/oauth/authorize
  accessTokenUrl=${securesocial.gitlab.baseUrl}/login/oauth/access_token
  // The OAUTH Client ID
  clientId=YOUR-GITLAB-CLIENT-ID
  // The OAUTH Client secret
  clientSecret=YOUR-GITLAB-CLIENT-SECRET 
}
```

After the change, restart codatlas process:

```bash
./lambda-compose restart codatlas
```

Go back to your browser and go to Insight.io Home Page, click on Login button on the top right, and then click on Login with Gitlab, make sure you can successfully login with your Gitlab account.


**Integration With LDAP**

Insight.io also support integration with `LDAP` to support user authentication. This section describes how to integrated with both `LDAP` and `Gitlab`.

To start with, you need to have a functional LDAP server and a Gitlab server. The first step is to integrated Gitlab with LDAP, which has been described by [Gitlab Docs](https://docs.gitlab.com/ce/administration/auth/ldap.html).

After integrating Gitlab with LDAP, we can now start to integrate Insight.io into the stack. Log into your Gitlab admin account and goto `Profile Settings`, then click on the `Account` tag to get your `Private Token`.

Go back to the bash terminal, open and edit the `user.conf` file:

```bash
vi ./lambdalab-docker/configs/user.conf
```

Configure the `ldap` section under `securesocial` like following:

```json
securesocial {

  ldap {
    
    //  Configurations of other components that integrates with LDAP.
    integration {
      // Gitlab integration.   
      gitlab {
        // Gitlab host url.
        gitlabUrl = "YOUR-GITLAB-URL"
        
        // Gitlab administrator account's private token.
        rootPrivateToken = ""
      }
    }

    //  the full url of the ldap server, including protocal, hostname and port
    //  e.g. "ldaps://localhost:636" , "ldap://localhost:389"
    providerUrl="ldap://localhost:389"

    //  search base from which the employee will be searched from
    searchBase="dc=example,dc=com"

    //  whether to use ssl when search ldap directory
    //  usually if it is turned on, providerUrl should starts with ldaps protocal with 636 port
    //  Also note that if your server is using a self-signed CA, add the CA into the keystore of your jvm otherwise
    //  there will be an SSL handshake error
    // useSsl=true
  }

}
```

After the change, restart codatlas process:

```bash
./lambda-compose restart codatlas
```

Go back to your browser and go to Insight.io Home Page, click on Login button on the top right, and the login information should have changed from `Email` to `LDAP Username`, which means you have successfully configured LDAP authentication. Enter your LDAP credentials and you should be abled to login.

You are done with integrate Insight.io with Gitlab! Please refer to User Manual for details on how to use it.
