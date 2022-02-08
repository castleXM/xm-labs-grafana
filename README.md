# Grafana
Grafana is an open source metric analytics & visualization suite. It is most commonly used for visualizing time series data for infrastructure and application analytics but many use it in other domains including industrial sensors, home automation, weather, and process control. This integration extends the ability to alert the person on call to a group and pause or unpause an alert coming out of Grafana using our closed-loop integration. Check out the sweet video!


[![Grafana Integration](https://img.youtube.com/vi/Dj2sEaZzXi0/0.jpg)](https://www.youtube.com/watch?v=Dj2sEaZzXi0&feature=youtu.be)

---------

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

---------

An updated version of this integration is available. You can install the new one-way version right from the Workflow Templates directory within your xMatters instance. [Learn more](http://help.xmatters.com/integrations/#cshid=Grafana).

---------

# Pre-Requisites
* [Grafana](https://grafana.com/)
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [GrafanaAlert.zip](GrafanaAlert.zip) - Workflow containing the Grafana Steps. 

# How it works
An alert fires a webhook to the xMatters Workflow HTTP Trigger. The HTTP Trigger parses the incoming JSON and builds the event, then fires the event to notify the default recipients. Alternatively [subscriptions](http://help.xmatters.com/OnDemand/userguide/receivingalerts/subscriptions/howtousesubscriptions.htm) can be set up to notify the desired parties. From the alert, you can pause the alert in Grafana to investigate the issue. When the issue is fixed, you can resume the alerting rule. When the alerting status of the Grafana alert goes to "ok", then the flow terminates the existing xMatters events.

# Installation

## xMatters set up
1. Login as the integration user in xMatters and navigate to the Developer Tab. (NOTE: Make sure the integration user has **REST Web Services User** Role. Reference General Notes section on how to create API user in xMatters.
2. Import the [GrafanaAlert.zip](GrafanaAlert.zip) Steps to a workflow.
3. Click on the workflow, and then Edit>Layout on the Grafana Alert to modify the alert recipients.
<details>
  <summary>Click for image</summary>
  <img src="media/GrafanaGroup.png" height=300 />
</details>

4. Save changes and return to the previous page. Click on Flows, and then Grafana Alert.
<details>
  <summary>Click for image</summary>
  <img src="media/FlowDesigner.png" height=300 />
</details>

5. Select the "Grafana Alert - Inbound from Grafana" step.
<details>
  <summary>Click for image</summary>
  <img src="media/StepLocation.png" height=300 />
</details>

6. Copy the Initiation URL, this will be used for setting up an Alert Notification Channel in Grafana.
<details>
  <summary>Click for image</summary>
  <img src="media/InitiationURL.png" height=300 />
</details>

7. Insert the API Key you generated in Grafana into `Grafana Token` constant, Which is accessible in the Flow Designer under Components>Constants. Reference [General Notes](#general-notes) section on how to generate the API key 
<details>
  <summary>Click for image</summary>
  <img src="media/GrafanaTokenConstant.png" height=300 />
</details>


8. Add the Grafana Endpoint by clicking on Components>Endpoints in the Flow Designer. Add an endpoint and name it "Grafana". Add the URL to your Grafana instance. Make sure you save changes. 
<details>
  <summary>Click for image</summary>
  <img src="media/GrafanaEndPoint.png" height=300 />
</details>

## Grafana set up
1. You first need to set up a notification channel in Grafana which can be found under the Alerting section
<details>
  <summary>Click for image</summary>
  <img src="media/CreateNotificationChannel.png" height=400 />
</details>


2. Click on "New Channel" and create a new webhook found under "type". Name it, set Http Method to "POST", set URL as the URL you saved. **Reference step 6 in the xMatters set up for the URL**. Your channel should look something like this. **NOTE**: If you want to test out and see if the webhook works, you can click "Send Test" at the bottom.
<details>
  <summary>Click for image</summary>
  <img src="media/GrafanaChannel.png" height=400 />
</details>


3. Go to the chart you want to be alerted on in Grafana, click "edit", click "Alert", then click "Notifications". Click the plus icon and add the Channel you just added in the previous step.
<details>
  <summary>Click for image</summary>
  <img src="media/AlertSectionGrafana.png" height=400 />
</details>


## General Notes
* How to set up the Grafana API Key to plug into xMatters. **PLEASE NOTE: Grafana will only show the API you created ONCE. Suggestion is to copy and paste it in a notepad somewhere so you can get to it if you ever need it again**
<details>
  <summary>Click for image</summary>
  <img src="media/APIKeysGrafana.png" height=400 />
</details>

* How to create API User in xMatters
Click "Users", click "Invite Users" or "Add Users". Information should be something like this.
<details>
  <summary>Click for image</summary>
  <img src="media/RESTAPIUser.png" height=500 />
</details> 
If it requires an email, the email can be something like email@xmatters.com 

# Testing
Do an action in your Grafana application or infrastructure that will trigger the alert conditions set up in the Alert. This will fire the webhook into the workflow and an event will be created, targeting the default recipients. After it targets the right person, you can use our 2-way integration by responding with "Pause Alert" to pause the alerting process in Grafana. Once you fix the issue in Grafana, you can come back to the original xMatters alert and use the response option "Resume Alert" to resume the alerting rule.

<details>
  <summary>Click for image</summary>
  <img src="media/GrafanaAlert1.png" height=500 />
</details>

# Troubleshooting
If it doesn't work, then access the log to find out what's going wrong.

Click the Activity button in the upper right of the screen.

<details>
  <summary>Click for image</summary>
  <img src="media/Activity.png" height=400 />
</details>

Select a flow element such as "Grafana Alert - Inbound from Grafana".

<details>
  <summary>Click for image</summary>
  <img src="media/ActivityAlert.png" height=400 />
</details>

Select "Log" in order to view the log.

<details>
  <summary>Click for image</summary>
  <img src="media/ActivityLog.png" height=400 />
</details>
