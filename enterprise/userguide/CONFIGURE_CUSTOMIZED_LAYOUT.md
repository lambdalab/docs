# Configure Customized Layout

The layout of our frontend now can be customized by adding an additional sidebar on the left and a navigational bar on the top. Follow the following steps to enable it.  


## Enable Layout Customization

In file `configs/lambdalab-enterprise.conf`, flip the `frontendConfig.enableCustomization` config item:

```
...
codatlas: {
    ...
    frontendConfig.enableCustomization: true
    ...
}
...
```

By enable this config, 2 `div` are added into the html source: `div#customized-nav-bar`, `div#customized-side-bar`. These
2 `div` are the place where you can hook your own style or layout.

## Hook Your Content:

Also in file `configs/lambdalab-enterprise.conf`, you can config the `extraHeader` and `extraBody` fields to embed your
actual code to manipulate the 2 `div`.

```
...
codatlas: {
    ...
    extraHeader: "<link rel="stylesheet" type="text/css" href="your css file path">"
    extraBody: "<script type="text/javascript" src="your javascript file path"></script>"
    ...
}
...
```

Inline style and script also works.

## Hook User Profile for Tracking

Our user behavior tracking need to bind user profile into our tracker. However, by customizing our frontend, we are
assuming that you are going to use external user system instead of Insight.io's. So you have to manually bind user
profile into our tracker by adding the following code into your javascript file hooked into the html.

```
if (window.tracker) {
  var userId = 'user0';
  var userProfile = {
    uid: 'user0',
    avatar: 'https://xxx/user0.png',
    name: 'John',
    email: 'john@xxx.com'
  };
  window.tracker.userProfile("mengwei", { a: "nihao" });
} else {
  console.log('No InsightIO tracker found.');
}
```

## Example by Putting Things Together

To achieve the layout below, your config in `configs/lambdalab-enterprise.conf` should look like:

<img width="1440" alt="screen shot 2018-03-13 at 10 14 51 pm" src="https://user-images.githubusercontent.com/11132316/37347265-63f11852-270c-11e8-825a-f0e447523dde.png">


```
codatlas: {
    ...
    frontendConfig.enableCustomization: true
    extraHeader: """<style>
    #root {
      width: 75%;
    }
    #container {
      display: flex;
      flex-direction: row;
    }
    #customized-nav-bar, #customized-side-bar {
      text-align: center;
      font-size: 2rem;
      line-height: 54px;
    }
    #customized-nav-bar {
      background-color: red;
      width: 100%;
      height: 54px;
      position: fixed;
      top: 0;
    }
    #customized-side-bar {
      flex-shrink: 0;
      writing-mode: tb-rl;
      background-color: green;
      width: 25%;
    }
  </style>"""
  extraBody: """<script type="text/javascript">
    const customizedNavBarId = 'customized-nav-bar';
    const customizedSideBarId = 'customized-side-bar';
    const $navBar = document.getElementById(customizedNavBarId);
    const $sideBar = document.getElementById(customizedSideBarId);
    console.log('Customized nav bar id is', customizedNavBarId);
    console.log('Customized side bar id is', customizedSideBarId);
    $navBar.appendChild(document.createTextNode('This is nav bar.'));
    $sideBar.appendChild(document.createTextNode('This is side bar.'));
    
    if (window.tracker) {
      var userId = 'user0';
      var userProfile = {
        uid: 'user0',
        avatar: 'https://xxx/user0.png',
        name: 'John',
        email: 'john@xxx.com'
      };
      window.tracker.userProfile("mengwei", { a: "nihao" });
    } else {
      console.log('No InsightIO tracker found.');
    }
  </script>"""
    ...
}
```

To explain a bit:

* In `frontendConfig.enableCustomization`, set to `true` to enable layout customization
* In `extraHeader`, you can place inline css styles for the additional 2 `div` (`div#customized-nav-bar` and
`div#customized-side-bar`). Try not to modify `#root` and `#container`.
* In `extraBody`, you can place inline javascript to manipulate the 2 `div`. Remember to set the profile of the tracker.
Otherwise, our frontend won't be able to bind the user to all the user behavior tracking.

