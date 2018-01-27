# Configure LDAP Integration

Insight.io can use LDAP for authentication with some simple configuration. You can configure these options in `user.conf` and uncomment the ldap section, as shown below:

```
  ldap {
    //  the full url of the ldap server, including protocal, hostname and port
    //  e.g. "ldaps://localhost:636" , "ldap://localhost:389"
    providerUrl="ldaps://localhost:636"

    //  search base from which the employee will be searched from
    //  e.g. searchBase="dc=example,dc=com"
    searchBase="dc=example,dc=com"

    //  the bindDn when performing search
    //  e.g. bindDn="cn=Directory Manager"
    bindDn="cn=Directory Manager"

    //  the password used together with the bindDn for authentication
    //  e.g. password="changeme"
    password="changeme"

    //  whether to use ssl when search ldap directory
    //  usually ssl is turned on, providerUrl should starts with ldaps protocal with 636 port
    //  Also note that if your server is using a self-signed CA, add the CA into the keystore of your jvm
    //  otherwise there will be an SSL handshake error
    useSsl=true

    //  the field that is used as user id field in search filter
    //  common field name are "uid" for OpenDJ and "sAMAccountName" for Microsoft AD
    //  if this option is not set, it is default to be "uid"
    uidFieldName = "uid"

    //  the attribute from LDAP response that will be used as the username in Insight.io
    //  A list of attribute names are allowed and the first avaiable attribute name will be used
    //  If you don't know what to be set, "uid, sAMAccount, userid" should cover most of the cases
    userNameFieldNames="uid, sAMAccount, userid"

    //  the attribute from LDAP response that will be used as the email in Insight.io
    //  If you don't know what to be set, "mail, email, userPrincipalName" should cover most of the cases
    emailFieldNames="mail, email, userPrincipalName"
  }

```
Alternatively, you can also setup the LDAP config in `$HOSTNAME/projects/admin`, the config set in the webpage will be stored in the databse and overwrite the one in config file.

Note that as long as `Provider URL` property is non-empty, LDAP log in will be enabled and normal username/password login will be disabled.

If your company's LDAP is using a self-signed CA, Insight.io will need to add the certificate into it's JVM truststore to enable SSL authentication. To do this, simply put the certificate the following folder:

```bash
lambdalab-docker/certs
```

This folder will be mounted into Insight.io container and all the certificate within will be added into Insight.io truststore.

## Disable UserPassword Authentication

To disable UserPassword authentication with LDAP authentication enable only, you can configure the options in `securesocial.conf` and uncomment the `userpass` section, as shown below:

```
securesocial {
...
//  userpass {
//    #
//    # Enable username support, otherwise SecureSocial will use the emails as user names
//    #
//    withUserNameSupport=false
//    sendWelcomeEmail=true
//    tokenDuration=60
//    tokenDeleteInterval=5
//    signupSkipLogin=true
//    minimumPasswordLength=6
//  }
...
}
```

## Enforce User Login

To enforce user login while browsing code, flip the `codatlas.frontendConfig.enableProjectPageLoginModal` to be true in `lambdalab-enterprise.conf`, as shown below:

```
codatlas: {
  ...
  frontendConfig.enableProjectPageLoginModal: true
  ...
}
```