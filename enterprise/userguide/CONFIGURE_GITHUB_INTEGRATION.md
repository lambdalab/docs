# Configure Github Integration

This section is only necessary if you want to integrate Insight.io with Github, it's highly recommended if you use Github as your code hosting service. 

Log into your github account and go to `Settings` then `OAuth applications` then `Developer applications` tab.

Click on `Register new application` button and fill in `Application name` and `Application description` section with preferred text. Fill in `Homepage URL` and `Authorization callback URL` with public DNS of the server, e.g. `http://ec2-52-35-135-191.us-west-2.compute.amazonaws.com`. Click `Register Application` to create a new OAuth application. Note `Client ID` and `Client Secret` Github provided with the newly created application.

Go back to the bash terminal, open and edit the `user.conf` file:

```bash
vi ./lambdalab-docker/configs/user.conf
```

And change ``ClientId`` and ``ClientSecret`` fields of both ``github-private`` and ``github`` sections to be the ``Client ID`` and ``Client Secret`` of your github application you just created:

```bash
github {
  baseUrl="https://github.com"
  authorizationUrl=${securesocial.github.baseUrl}/login/oauth/authorize
  accessTokenUrl=${securesocial.github.baseUrl}/login/oauth/access_token
  clientId=d1d8e43a14e1f3e1e2d8
  clientSecret=ac383f2f378015a06d8d55ef340a029d4314ec0f
  scope="user:email,public_repo"
}
```

**Notice**: Remember to uncomment the entire `github` section by removing the leading `#` in each line.

After the change, restart codatlas process:

```bash
./lambda-compose restart codatlas
```

Go back to your browser and go to Insight.io Home Page, click on `Login` button on the top right, and then click on `Login with Github`, make sure you can successfully login with your Github account.

You are done with integrate Insight.io with Github! Please refer to [New User Guide](../USER_GUIDE.md) for details on how to use it.
