![Na logo beta](https://github.com/tommasomoretti/nameless-analytics/assets/29273232/7d4ded5e-4b79-46a2-b089-03997724fd10)

An open source web analytics platform for power users based on [Google Tag Manager](https://marketingplatform.google.com/intl/it/about/tag-manager/) and [Google BigQuery](https://cloud.google.com/bigquery). 

Collect, analyze and activate your website data with a real-time web analytics suite that respects users privacy, for free.



## Main features
- **1° party data context**\
Cookies are released from server, in a first-party context and events data are saved in your own Google BigQuery dataset.

- **Privacy by design**\
You can automatically respects users choises or you can choose to track every event regards users consents. By default, no PII data are tracked.

- **Real-time**\
Data ingestion into Google BigQuery is nearly instantaneous and events are available within a couple of seconds.

- **Lightweight and blazing fast**\
The main library only weighs 2.9 kB and it's served via CloudFlare CDN. All hits are sent via HTTP POST request.

- **Cross-domain tracking**\
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.

- **Ecommerce tracking**\
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.

- **Single Page App ready**\
Track single page application pageviews easily, you can customize the tracker depending on your needs.

- **Server-side tracking**\
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras luctus libero ipsum, vestibulum egestas orci ullamcorper eget.

- **Multiple data type**\
Send integer, float, string or JSON formatted values. 



## Basic requirements
- Google Consent Mode installed on a website
- A client-side Google Tag Manager container installed on a website
- A server-side Google Tag Manager container hosted on App Engine or Cloud Run (Stape.io to be tested)
- A Google BigQuery dataset with write permissions

See [Get started section](https://github.com/tommasomoretti/nameless-analytics/blob/main/README.md#get-started) for details about how to setup server-side Google Tag Manager, the BigQuery main table and the whole environment.



## How it works
Here a basic schema and a brief explanation of how Nameless Analytics works.

![Nameless Analytics Schema](https://github.com/user-attachments/assets/cc837ffe-d3bf-4168-a87f-077f9f2ea847)


### Client-side Tracker Tag
When the Client-side Tracker Tag is loaded, if the ```respect_consent_mode``` option is enabled, the first tag that should be fired, checks the ```analytics_storage``` status.
- If ```analytics_storage``` is equal to granted, the tag sends the hit to the server-side Google Tag Manager endpoint, with the event name and event parameters configured in the tag.
  <img width="1263" alt="Nameless Analytics client-side logs" src="https://github.com/tommasomoretti/nameless-analytics/assets/29273232/bca94adf-cdf5-4bf3-bb41-e69461ba9b38">
  
- If ```analytics_storage``` is equal to denied, the tag waits until consent is granted. If consent is granted (in the context of the same page), all pending tags will be fired.
  <img width="1265" alt="Screenshot 2024-06-26 alle 15 35 47" src="https://github.com/tommasomoretti/nameless-analytics/assets/29273232/f5c8174c-3acb-44f4-8a84-33c03c794af8">
  
If the ```respect_consent_mode``` option is disabled, the tag fires regardless of the user's consent.

For more details, see [Nameless Analytics client side tag](https://github.com/tommasomoretti/nameless-analytics-client-tag)


### Server-side Client Tag
When the Server-side Tag Manager Client Tag receives the request, it checks if any cookies in there.

| Cookie name                | Example value                       | Default expiration | Description                                                                                     |
|----------------------------|-------------------------------------|--------------------|-------------------------------------------------------------------------------------------------|
| nameless_analytics_user    | 3135061696                          | 400 days           | Random number between 1000000000 and 9999999999                                                 |
| nameless_analytics_session | 3135061696_3983471069-1722607958646 | 30 minutes         | nameless_analytics_user + Random number between 1000000000 and 9999999999 + Last event timestamp|

- If no cookies are present or the ```nameless_analytics_user``` cookie is not set but ```nameless_analytics_session cookie``` is set, the client tag generates generates two values, one for ```nameless_analytics_user``` cookie and one for ```nameless_analytics_session``` cookie), adds these values as event parameters and sets two cookies with the response.

- If the ```nameless_analytics_user``` cookie is set but ```nameless_analytics_session cookie``` is not (session expires), the client tag generates generates only one value for ```nameless_analytics_session``` cookie, adds that value to the hit, as event parameters, set again the same ```nameless_analytics_user``` cookie and set the ```nameless_analytics_session``` cookie with the response.

- If both cookies are present, the tag does not create any new cookies but adds their values to the hit.

After that, the hit will be logged in a BigQuery event date partitioned table.

<img width="1512" alt="Nameless Analytics server-side logs" src="https://github.com/tommasomoretti/nameless-analytics/assets/29273232/776e0527-0b20-46d0-90d1-cac8064e6b10">

For more details, see [Nameless Analytics server side tag](https://github.com/tommasomoretti/nameless-analytics-server-tag)



## Get started
Read how to setup 
1. [Google Consent Mode installed](https://developers.google.com/tag-platform/security/guides/consent?hl=en&consentmode=advanced)
2. [Server-side Tag Manager](https://developers.google.com/tag-platform/tag-manager/server-side) with [Google App Engine](https://developers.google.com/tag-platform/tag-manager/server-side/app-engine-setup) or [Google Cloud Run](https://developers.google.com/tag-platform/tag-manager/server-side/cloud-run-setup-guide)
3. [Nameless Analytics Client-side Tracker Tag](https://github.com/tommasomoretti/nameless-analytics-client-tag)
4. [Nameless Analytics Server-side Client Tag](https://github.com/tommasomoretti/nameless-analytics-server-tag)
5. [Nameless Analytics main table and reporting queries examples](https://github.com/tommasomoretti/nameless-analytics-reporting-queries) in Google Big Query
6. [Google Looker Studio Dashboard example](https://lookerstudio.google.com/reporting/d4a86b2c-417d-4d4d-9ac5-281dca9d1abe/page/HPxxD)


### Do you want to see a live demo? 
Visit [namelessanalytics.com](https://namelessanalytics.com?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) or [tommasomoretti.com](https://tommasomoretti.com?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) and open the developer console.

---

Reach me at: [Email](mailto:hello@tommasomoretti.com) | [Website](https://tommasomoretti.com/?utm_source=github.com&utm_medium=referral&utm_campaign=nameless_analytics) | [Twitter](https://twitter.com/tommoretti88) | [Linkedin](https://www.linkedin.com/in/tommasomoretti/)
