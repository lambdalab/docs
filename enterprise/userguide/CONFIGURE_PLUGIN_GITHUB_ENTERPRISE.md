## Configure Insight.io Browser Plugin for GitHub Enterprise

At Insight.io, we have another well recognized product - **Insight.io for GitHub**
([Chrome](https://chrome.google.com/webstore/detail/insightio-for-github/pmhfgjjhhomfplgmbalncpcohgeijonh),
[Firefox](https://addons.mozilla.org/firefox/addon/insight-io-for-github/)) - aims to deliver the same code
intelligence experience, as we do by [Insight.io](https://insight.io), to [GitHub](https://github.com) code
browsing and search.

To make sure that our code intelligence experiences are universally accessible to developers, we tailored the
browser plugin particularly for enterprise working environment and pushed **Insight.io for GitHub Enterprise**.

#### [Download Chrome Plugin Here](https://chrome.google.com/webstore/detail/insightio-for-github-ente/dkceiholpippomlhdlhdogmelkplpchm)

**Note**: This plugin is currently available for Chrome only. We are in progress on bringing it to Firefox.
Also, this plugin won't be able to search on Chrome Web Store, you can only find it via the download link above.

### Prerequisites

Make sure your company has the following environment correctly setup: 

* GitHub Enterprise Instance: e.g. `https://github.example.com`
* Insight.io Enterprise Instance: e.g. `https://insightio.example.com'

### Setup

* Install **[Insight.io for GitHub Enterprise](https://chrome.google.com/webstore/detail/insightio-for-github-ente/dkceiholpippomlhdlhdogmelkplpchm)**.
* Visit [chrome-extension://dkceiholpippomlhdlhdogmelkplpchm/popout.html?gheUrl=https://github.example.com](chrome-extension://dkceiholpippomlhdlhdogmelkplpchm/popout.html?gheUrl=https://github.example.com)
to let the plugin be aware of the GitHub Enterprise instance in your environment.
* Make sure you've login on your Insight.io Enterprise instance already.
* Provide your Insight.io Enterprise url to plugin in the **Settings** tab as below and click **Save**.
![image](https://user-images.githubusercontent.com/987855/36393877-5dca58e2-1566-11e8-8f80-6b4c82d64bca.png)












