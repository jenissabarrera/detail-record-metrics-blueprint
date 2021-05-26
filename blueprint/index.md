---
title: Generate Analytics Detailed Record Metrics
author: jenissa.barrera
indextype: blueprint
icon: blueprint
image: 
category: 
summary: |
  This Genesys Cloud Developer Blueprint provides instructions for getting Detailed Records using the Analytics API. There are three perspective of data in Analytics API. Instantaneous Observations, Aggregate Metrics and Detailed Records. This blueprint will focus on the detailed records. 
---

This Genesys Cloud Developer Blueprint provides instructions for getting Detailed Records using the Analytics API. There are three perspective of data in Analytics API. Instantaneous Observations, Aggregate Metrics and Detailed Records. This blueprint will focus on the detailed records.

![Flowchart](images/flowchart.jpg "Flowchart")

## Definitions

* **Analytics Query Builder** - The Analytics Query Builder developer tool provides a user interface that simplifies the creation of analytics queries. You pick the analytics criteria. The tool generates an analytics query that it runs against the Genesys Cloud Analytics API and returns a query result from your Genesys Cloud organization. You can use the JSON in the generated query in your own application.
* **Detailed Record Metrics** - Audit style records that capture a very fine-grained level of detail around user (e.g. agent) and customer interactions.


## Requirements

Implementing this solution requires experience in several areas or a willingness to learn:

- Administrator-level knowledge of Genesys Cloud and the Genesys AppFoundry
- Genesys Cloud Platform API knowledge


### Genesys Cloud account requirements

This solution requires a Genesys Cloud license. For more information on licensing, see [Genesys Cloud Pricing](https://www.genesys.com/pricing "Opens the pricing article").

A recommended Genesys Cloud role for the solutions engineer is Master Admin. For more information on Genesys Cloud roles and permissions, see the [Roles and permissions overview](https://help.mypurecloud.com/?p=24360 "Opens the Roles and permissions overview article").


### Procedure
1. Login to the web app version of your Genesys Cloud organization.
2. Open the Analytics Query Builder developer tool.
3. From the Query Type menu, select Conversation Detail or User Data.
  ![Analytics Query Builder](images/analytics-query-builder.jpg "Analytics Query Builder")

4. Add start and end date for the date range of the of the query.

  For the user data, if you selected the default properties of the query the result will be this. 

   ![User Query](images/standard-user-query-result.jpg "Standard User Query")


    Some of the generated results are user id and primary presence. In the system presence key under the primary presence, this is where the availability of the agent shows. The start and end time of the specific availability is also available. Basically, how the statuses of an agent looks like for a specific time and day.

   ```json
   {
  "primaryPresence": [
        {
          "startTime": "2021-04-26T15:55:52.163Z",
          "endTime": "2021-04-26T16:26:20.851Z",
          "systemPresence": "AVAILABLE",
          "organizationPresenceId": "6a3af858-942f-489d-9700-5f9bcdcdae9b"
        },
        {
          "startTime": "2021-04-26T16:26:20.851Z",
          "endTime": "2021-04-26T20:37:00.083Z",
          "systemPresence": "OFFLINE",
          "organizationPresenceId": "ccf3c10a-aa2c-4845-8e8d-f59fa48c58e5"
        },
        {
          "startTime": "2021-04-26T20:37:00.083Z",
          "endTime": "2021-04-26T21:36:53.702Z",
          "systemPresence": "AVAILABLE",
          "organizationPresenceId": "6a3af858-942f-489d-9700-5f9bcdcdae9b"
        },
        {
          "startTime": "2021-04-26T21:36:53.702Z",
          "systemPresence": "OFFLINE",
          "organizationPresenceId": "ccf3c10a-aa2c-4845-8e8d-f59fa48c58e5"
        }
      ]
   }
   ```

   Routing Status data is also available which shows the history of interaction of agents and the start and end time stamps of the interaction.

      ```json
   {
  "primaryPresence": [
        {
          "startTime": "2021-04-26T15:55:52.163Z",
          "endTime": "2021-04-26T16:26:20.851Z",
          "systemPresence": "AVAILABLE",
          "organizationPresenceId": "6a3af858-942f-489d-9700-5f9bcdcdae9b"
        },
        {
          "startTime": "2021-04-26T16:26:20.851Z",
          "endTime": "2021-04-26T20:37:00.083Z",
          "systemPresence": "OFFLINE",
          "organizationPresenceId": "ccf3c10a-aa2c-4845-8e8d-f59fa48c58e5"
        },
        {
          "startTime": "2021-04-26T20:37:00.083Z",
          "endTime": "2021-04-26T21:36:53.702Z",
          "systemPresence": "AVAILABLE",
          "organizationPresenceId": "6a3af858-942f-489d-9700-5f9bcdcdae9b"
        },
        {
          "startTime": "2021-04-26T21:36:53.702Z",
          "systemPresence": "OFFLINE",
          "organizationPresenceId": "ccf3c10a-aa2c-4845-8e8d-f59fa48c58e5"
        }
      ]
   }
   ```

    The user can also modify the search and add a specific filter. In this case, we will search for available agents and interacting agents. To do so, go to Presence filters, in the predicates section click on dimension and choose systemPresence. Choose available as value. 

    ![System Presence Available](images/system-presence-available.jpg "Sytem Presence Available")

    For the Routing Status, go to Routing Status Filters. Select or as type. Under the predicates value choose dimension, on the dimension choose Routing Status. And select Interacting as Value.

    ![Routing Status Interaction](images/routing-status-interacting.jpg "Routing Status Interacting")

    This is the result when the filters are applied, other data will be filtered out. This will make the result straightforward depending on the user need.

    ![Available and Interacting Query Result](images/available-and-interacting-query-result.jpg "Available and Interacting Query Result")

  For the conversation data, this is where the detail of every conversation will be generated. This will generate data like, name, ANI, direction and metrics. Take note that every conversation has a different properties.

    ![Standard Conversation Query Result](images/standard-conversation-query-result.jpg "Standard Conversation Query Result")

     The user can also modify the search and add specific filter. In this case, we will search for inbound and voice data. To do so, go to Segment filters, in the predicates section click on type and select Dimension. On the dimension select value. And on the value field type in inbound. For the voice filter add another predicate. Select dimension as type and select direction for dimension. Type voice on the value field.

     ![Voice and Inbound Conversation Query](images/voice-and-inbound-conversation-query.jpg "Voice and Inbound Conversation Query")

    Same with the previous result, the generated data is personalized once filtered out. 
    
     ![Voice and Inbound Conversation Query Result](images/voice-and-inbound-conversation-query-result.jpg "Voice and Inbound Conversation Query Result")

5. Once done with the properties modification, the user can now copy the generated query and use it for their application.

![Generated Query](images/generated-query.jpg "Generated Query")

    
## Additional Resources
* [Genesys Cloud Developer Center](https://developer.mypurecloud.com/)
* [Analytics Query Builder developer tool quick start](https://developer.mypurecloud.com/gettingstarted/developer-tools-analytics-query.html)
* [Analytics Overview](https://developer.mypurecloud.com/api/rest/v2/analytics/overview.html#:~:text=Genesys%20Cloud%20provides%20a%20rich,performance%20and%20customer%2Fagent%20interactions.)




