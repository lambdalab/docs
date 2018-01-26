
## Config tracker

#### enable
Enable logstash/other adapter in config (in user.conf):
```
codatlas: {
  frontendConfig.enableLogstashTracker: true,
  frontendConfig.logstashUrl: "$url"
}
```
`$url` can be any http endpoint, eg:  http://mylogstashserver. Noted that even we by default use logstash to collect event, the endpoint could be anyone that accept the 
 request with specific format.

> endpoint must support cors if domain is not codatlas
> endpoint must be https if codatlas is running https

#### Schema
endpoint will receive http post requests as following:

```
{
      event: eventName, // name of the event
      userId: , // id of the event
      alias: , // a random userId before current user logged in
      user:  {
         uid, 
         email,
         name,
         ...
      },
      userAgent: navigator.userAgent,
      href: location.href, 
      screenWidth: screen.width,
      screenHeight: screen.height,
      referrer: document.referrer
      eventProps: {  // props of detail events
      }
      
}
```



