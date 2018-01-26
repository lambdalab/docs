## Token Usage

{% method %}
Whenever your have a token, you can talk to Insight.io via REST api without explicit authentication process. Attach the token in `token` query parameter and you should be able to pass the authentication and get your desired response.


{% sample lang="http" %}
**Usage**
```bash
$ curl -v https://insight.io/api/user/recentFiles?token=<your api access token>
```

{% common %}
**Response**

If you provide the correct token, you should get the desired response:

```json
HTTP/1.1 200 OK
[
  {
    "id":"github.com/aws/aws-sdk-java",
    "name":"aws-sdk-java",
    "timeStamp":1496358397966,
    "revision":"1.11.105",
    "path":"aws-java-sdk-cloudhsm/src/test/java/com/amazonaws/services/cloudhsm/smoketests/RunCucumberTest.java"
  },
  {
    "id":"github.com/aws/aws-sdk-java",
    "name":"aws-sdk-java",
    "timeStamp":1496358392087,
    "revision":"1.11.105",
    "path":"aws-java-sdk-core/src/main/java/com/amazonaws/AmazonWebServiceRequest.java"
  }
]
```

Otherwise, you will get error.

```json
HTTP/1.1 401 Unauthorized
{
  "error":"Credentials required"
}
```
{% endmethod %}