# Configure SAML Integration

This section is only necessary if you want to configure Insight.io to work with a SAML based SSO provider.

First you have to obtain IdP Metadata XML file from your SSO provider and place it under `$LAMBDA_HOME/samlMetadata`

Go back to the bash terminal, open and edit the `user.conf` file:

```bash
vi ./lambdalab-docker/configs/user.conf
```

uncomment the following line and set the value to be the folder containing the SAML IdP metadata XML file.

```bash
#codatlas.samlMetadata = ${LAMBDA_HOME}/samlMetadata
}
```

After the change, restart codatlas process:

```bash
./lambda-compose restart codatlas
```
You would also have to provide the following information regarding insight.io to your SMAL IdP:

```
ACS URL: ${hostname}/authenticate/saml
Entity ID: insight.io
```

