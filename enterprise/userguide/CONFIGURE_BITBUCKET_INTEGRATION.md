# Configure BitBucket Server (Stash) Integration

*This integration is for Atlassian [BitBucket Server](https://www.atlassian.com/software/bitbucket/server) (a.k.a. Stash), not for
[bitbucket.org](https://bitbucket.org), which is the online SaaS version.*

*We also have a quick video tutorial demonstrate the following step in [here](https://drive.google.com/file/d/1T8GcazIHOSSar9-LEM92o_WQNsF2MJxz/view?usp=sharing).*

## Prerequisites
1. Generate a RSA private key
```
openssl genrsa -out insightio.private.pem 1024
```
and the output file should look similar to
```
-----BEGIN RSA PRIVATE KEY-----
MIICXgIBAAKBgQDZpkwjYhaLA5P86AJsDrdAkgLb4Q1wlvV4Fk2ft1AEi1AW5YkU
ZwLx7t+3CRCRxdap7ZzJM+BtdRKu8AM8dEXY2eQeF4qEJVI/O4z1emnmG5oMQl/U
GEa9NY1Fip/aEWVLGeOydS7sl/H8TV6jd7EDiNBLx03ujp9k9qbUlGFBPQIDAQAB
AoGBANgeXTQ1ThUztFtJNj5+TlD7q4MScfn+rDhWTTXvHLGmdByISBnOQApkHBjw
E1fsjz+lBi50KMIHokm7YjtBaagYmISkfMqFesNU7hs/RjOeNAf65FWSfq8t3C5E
+7FL2gpvx7mbOHI5fSBa4wzHA/mOxndmzv3ojinh7k/+3pGBAkEA/ZQBrEQCKgU9
kKnIw2UlLmfLfHUek6+g8nCL21kkWCFveL6hav2J+lL/885lY76tB434IQxPN3oL
i+CcEYFWuQJBANu6ckCANqmxFK1aKlljD332u6PFCVxqqrqQALG1HdTJ+laAyHTS
73TCNczH3l3meJvJ+TZ6YJre+ISQXdC5PKUCQQDphSCZRLP9gH/2tfSVxJKeDqX9
AlpbRTThrzWMlaX7pybhuiQqxDwJk9/z5VHHrnPn7hzgSla1TyZM9VakZEi5AkEA
gsKU5W+nmBqKvJMQ6rr56DNh/Rbv+DB+Q6IY16h6BTzhnoLrSCKTX/+HdsNmwKi8
E7IBffsb7G5OpM0pF2J1BQJATbedk1hvLDmVeR0JvkphO7WqnZe13elBQgJ4Ubwn
RahDkYUV9DnCxMN8UGZHAssFYi/yQ9wJPuEdyBfNjUAsQA==
-----END RSA PRIVATE KEY-----
```
2. Generate a RSA public key with the private key file you have just created by
```
openssl rsa -pubout -in insightio.private.pem -out insightio.public.pem
```
And the output file should be similar to
```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDZpkwjYhaLA5P86AJsDrdAkgLb
4Q1wlvV4Fk2ft1AEi1AW5YkUZwLx7t+3CRCRxdap7ZzJM+BtdRKu8AM8dEXY2eQe
F4qEJVI/O4z1emnmG5oMQl/UGEa9NY1Fip/aEWVLGeOydS7sl/H8TV6jd7EDiNBL
x03ujp9k9qbUlGFBPQIDAQAB
-----END PUBLIC KEY-----
```

## Configure OAuth on BitBucket Server
1. Login with `admin` account on your BitBucket Server and find the *Application Links* settings in *Administration* page (/plugins/servlet/applinks/listApplicationLinks)
  ![image](https://user-images.githubusercontent.com/987855/35079954-95f31c5c-fc45-11e7-8873-1fc5b8de4a54.png)
2. Create a new link and provide the Insight.io Enterprise link in the popout modal.
  ![image](https://user-images.githubusercontent.com/987855/35080038-1bce3186-fc46-11e7-8c76-20391cc9c018.png)
3. Configure the setting for link application with all OAuth1 settings. Also, remember to opt-in the incoming link checkbox.
  ![image](https://user-images.githubusercontent.com/987855/35110185-286b5faa-fcb3-11e7-91d5-7e6ec38e7cc3.png)
4. Provide details for outgoing link as follows. The most important step is the public key section, in which you should fill in the content of your public key you have generated in *Prerequisites* section.

  **Notice**: Before copy the public key, remove the `-----BEGIN PUBLIC KEY-----` and `-----END PUBLIC KEY-----` header and **join the rest of the key into 1 single line**.
  ![image](https://user-images.githubusercontent.com/987855/35110275-5a2093b2-fcb3-11e7-8247-115be06148ba.png)
5. After you have created the application link, there is one last thing left. Edit the new create application link and in the *Incoming Authentication* tab, delete it and recreated it, but with *Consumer Callback URL* provided.
  ![image](https://user-images.githubusercontent.com/987855/35110713-74784fd8-fcb4-11e7-8d5e-f0760fd4f9f6.png)


## Integrate BitBucket Server OAuth1 with Insight.io Enterprise
In your `lambdalab.conf` file, add a new `bitbucket` section into the `securesocial` section with the following fields:
* `baseUrl`: the host of the BitBucket server instance
* `requestTokenUrl`, `accessTokenUrl` and `authorizationUrl` are the 3 separate links OAuth1 required and also the ones you have provided when setting up the application link
* `consumerKey` is the key for the OAuth1 secret
* `privateKey` is the content of the private key you have generated at the very beginning of this tutorial.

**Notice**: Before copy the private key, remove the `-----PRIVATE PUBLIC KEY-----` and `-----PRIVATE PUBLIC KEY-----` header and join the rest of the key into 1 single line. (A helpful command line for joining multiple lines together into one single line is `cat xxx.pem | xargs | sed "s/ //g"`).

```
bitbucket {
  baseUrl="http://bitbucket-server-5-6.insight.io"
  requestTokenUrl=${securesocial.bitbucket.baseUrl}/plugins/servlet/oauth/request-token
  accessTokenUrl=${securesocial.bitbucket.baseUrl}/plugins/servlet/oauth/access-token
  authorizationUrl=${securesocial.bitbucket.baseUrl}/plugins/servlet/oauth/authorize
  consumerKey=insightio
  privateKey="MIICXgIBAAKBgQDZpkwjYhaLA5P86AJsDrdAkgLb4Q1wlvV4Fk2ft1AEi1AW5YkUZwLx7t+3CRCRxdap7ZzJM+BtdRKu8AM8dEXY2eQeF4qEJVI/O4z1emnmG5oMQl/UGEa9NY1Fip/aEWVLGeOydS7sl/H8TV6jd7EDiNBLx03ujp9k9qbUlGFBPQIDAQABAoGBANgeXTQ1ThUztFtJNj5+TlD7q4MScfn+rDhWTTXvHLGmdByISBnOQApkHBjwE1fsjz+lBi50KMIHokm7YjtBaagYmISkfMqFesNU7hs/RjOeNAf65FWSfq8t3C5E+7FL2gpvx7mbOHI5fSBa4wzHA/mOxndmzv3ojinh7k/+3pGBAkEA/ZQBrEQCKgU9kKnIw2UlLmfLfHUek6+g8nCL21kkWCFveL6hav2J+lL/885lY76tB434IQxPN3oLi+CcEYFWuQJBANu6ckCANqmxFK1aKlljD332u6PFCVxqqrqQALG1HdTJ+laAyHTS73TCNczH3l3meJvJ+TZ6YJre+ISQXdC5PKUCQQDphSCZRLP9gH/2tfSVxJKeDqX9AlpbRTThrzWMlaX7pybhuiQqxDwJk9/z5VHHrnPn7hzgSla1TyZM9VakZEi5AkEAgsKU5W+nmBqKvJMQ6rr56DNh/Rbv+DB+Q6IY16h6BTzhnoLrSCKTX/+HdsNmwKi8E7IBffsb7G5OpM0pF2J1BQJATbedk1hvLDmVeR0JvkphO7WqnZe13elBQgJ4UbwnRahDkYUV9DnCxMN8UGZHAssFYi/yQ9wJPuEdyBfNjUAsQA=="
}
```

Then restart the codatlas service by `./lambda-compose restart lambda_codatlas`.

## (Optional) Configure OAuth with BitBucket Server Admin User Personal Access Token

(This section is optional)

To let BitBucket Server grant Insight.io with higher level of permission, you can attach personal access token of the Admin user to Insight.io. Follow the steps below to achieve this:

1. Login with `admin` account on your BitBucket Server and find the *Personal Access Token* settings in *Account* page (/account).
![image](https://user-images.githubusercontent.com/987855/36080840-86517456-0f4b-11e8-8cd6-6a51e4af05e5.png)
2. Create a new token by clicking the "Create a token" button on the top right.
3. Provide at least *Write* permission for both *Projects* and *Repositories*.
![image](https://user-images.githubusercontent.com/987855/36080856-bd65ab6a-0f4b-11e8-9aa6-45bbf7b7f8f8.png)
4. Keep the new created token
![image](https://user-images.githubusercontent.com/987855/36080903-7ee6c49a-0f4c-11e8-8805-667c24d24489.png)
5. Add two additional fields `adminUsername` and `adminToken` in the `bitbucket` section as mentioned above. Then
the entire `bitbucket` section should look like:

```
bitbucket {
  ...
  consumerKey=xxx
  privateKey=xxx
  adminUsername=admin
  adminToken="NTI0NTI3NDE3NDQzOmPP6AuBAbdhJntXn1fHXW+Tlu77"
}
```

## Verify the Integration
If everything works well, you should be able to see *Login with BitBucket* button in login page. Click on it to kick off the standard OAuth1 authentication process.

After you have logged in, visit `/account/projects` page of Insight.io Enterprise instance and open the *Import Projects* modal and you should be able to see all the projects that are visible to you on BitBucket server.