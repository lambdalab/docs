# Configure SAML Single Sign On Integration

You can setup Insight.io to work with your SAML based Single Sign On service provider such as Google for Work or Okta. 

To enable SAML Single Sign On, first create a SAML 2.0 application entry with your provider. During the creation, there are two mandatory settings: `ACS URL` (`Single Sign on URL`) and `Entity ID` (`Audience URI`). Set the setting as following:

`ACS URL` ： `https://$HOSTNAME/authenticate/saml`

`Entity ID` ： `https://$HOSTNAME`

You also need to setup up attribute mapping for `email` field as email is required to create a account in Insight.io. If the attribute `email` is not correctly set, you will see an error of `email is not present in SAML attributes` in console output.

Note that `https://$HOSTNAME` should be the same with `codatlas.frontendUrl` property in `lambdalab-enterprise.conf`. As a matter of fact, if `codatlas.frontendUrl` property does not start with `https` when SAML is enabled, Insight.io will throw an error message.

After the SAML application is created, make sure to download the IDP Metadata XML file. Put the XML file under the following folder:

`lambdalab-docker/samlMetadata/`

Lastly, open `lambdalab-enterprise.conf` and uncomment the following line and point it to the IDP Metadata XML file：

```
  // samlMetadata: ${LAMBDA_HOME}/samlMetadata/METADATA_IDP.XML
```
Save and close the config file and restart web server. Note that when SAML is enabled, other login methods (GitHub, LDAP etc.) will be disabled.