![Na logo beta](https://github.com/tommasomoretti/nameless-analytics/assets/29273232/7d4ded5e-4b79-46a2-b089-03997724fd10)

An open source analytics platform for power users based on [Google Tag Manager](https://marketingplatform.google.com/intl/it/about/tag-manager/) (both client-side and server-side) and [Google BigQuery](https://cloud.google.com/bigquery). 

Collect, analyze and activate your website data with a flexible analytics suite that lets you respect user privacy, for free.


## Main features
- **1° party data storage**\
Event data is saved in a own Google Cloud project. Cookies are released in a first-party context, in a secure and inaccessible mode to third parties.

- **Privacy-focused**\
By default, no PII data is tracked, but you can add it, if your users consent. You can choose if track every event or automatically respects user consent.

- **Real-time**\
Data insertion into Google BigQuery is nearly instantaneous and events are available within a couple of seconds.

- **Light-weight**\
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.

- **Client-side tracking**\
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.

- **Server-side tracking**\ 
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.


## Basic requirements
- Google client-side Tag Manager installed on a website
- Google server-side Tag Manager hosting on app engine or cloud run (Stape.io da testare)
- Google BigQuery dataset with write permissions

See [Get started section](https://github.com/tommasomoretti/nameless-analytics/blob/main/README.md#get-started) for details about how to setup server-side Google Tag Manager, the BigQuery main table and the whole environment.


## How it works
When a user land on your site, the first tag that fire checks the analytics_consent status. If it's denied, the tag waits until the consent is granted. If the consent is granted the tag fires, it loads the required libraries, set an event listener if cross-domain is enabled and sends the event to server-side Google Tag Manager's endpoint. 

When the server-side Tag Manager client tag receives the request, it checks if there are any cookies. If they are not set, the client tag generates 2 valius (one is the client id for nameless_analytics_user cookie and the other is the session id for nameless_analytics_session cookie). If the client_cookie is sets but there is no session_cookie 

Do you want to see a live demo? Visit [namelessanalytics.com](https://namelessanalytics.com?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) or [tommasomoretti.com](https://tommasomoretti.com?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) and open the developer console.

<img width="1263" alt="Nameless Analytics client-side logs" src="https://github.com/tommasomoretti/nameless-analytics/assets/29273232/bca94adf-cdf5-4bf3-bb41-e69461ba9b38">

In server-side Google Tag Manager you will see something like this:

<img width="1512" alt="Nameless Analytics server-side logs" src="https://github.com/tommasomoretti/nameless-analytics/assets/29273232/776e0527-0b20-46d0-90d1-cac8064e6b10">


## Get started
Read how to setup 
1. Server-side Tag Manager  with [Google App Engine](https://developers.google.com/tag-platform/tag-manager/server-side/app-engine-setup) or [Google Cloud Run](https://developers.google.com/tag-platform/tag-manager/server-side/cloud-run-setup-guide)
2. [Nameless Analytics client side tag](https://github.com/tommasomoretti/nameless-analytics-client-tag)
3. [Nameless Analytics server side tag](https://github.com/tommasomoretti/nameless-analytics-server-tag)
4. [Nameless Analytics main table]() in Google Big Query

---

Reach me at: [Email](mailto:hello@tommasomoretti.com) | [Website](https://tommasomoretti.com/?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) | [Twitter](https://twitter.com/tommoretti88) | [Linkedin](https://www.linkedin.com/in/tommasomoretti/)
