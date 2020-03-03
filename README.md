# Grafana
Grafana is an open source metric analytics & visualization suite. It is most commonly used for visualizing time series data for infrastructure and application analytics but many use it in other domains including industrial sensors, home automation, weather, and process control. This integration extends the ability to alert the person on call to a group and pause or unpause an alert coming out of Grafana using our closed-loop integration. Check out the sweet video!


[![Grafana Integration](https://img.youtube.com/vi/Dj2sEaZzXi0/0.jpg)](https://www.youtube.com/watch?v=Dj2sEaZzXi0&feature=youtu.be)

---------

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

---------

# Pre-Requisites
* [Grafana](https://grafana.com/) version >=4.4.3
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [GrafanaAlert.zip](GrafanaAlert.zip) - Communication Plan containing the Inbound and Outbound integration with form templates

# How it works
An alert fires a webhook to the xMatters Workflow HTTP Trigger. The HTTP Trigger parses the incoming JSON and builds the event, then fires the event to notify the default recipients. Alternatively [subscriptions](http://help.xmatters.com/OnDemand/userguide/receivingalerts/subscriptions/howtousesubscriptions.htm) can be set up to notify the desired parties. From the alert, you can pause the alert in Grafana to investigate the issue. When the issue is fixed, you can resume the alerting rule.  

# Installation

## xMatters set up
1. Login as the integration user in xMatters and navigate to the Developer Tab. (NOTE: Make sure the integration user has **REST Web Services User** Role. Reference General Notes section on how to create API user in xMatters.
2. Import the [GrafanaAlert.zip](GrafanaAlert.zip) Steps to a workflow.
3. Click on the workflow, and then Edit>Layout on the Grafana Alert to modify the alert recipients.
<kbd>
  <img src="media/GrafanaGroup.png" height=500>
</kbd>

4. Save changes and return to the previous page. Click on Flows, and then Grafana Alert.
<kbd>
  <img src="media/FlowDesigner.png">
</kbd>

5. Select the "Grafana Alert - Inbound from Grafana" step.
<kbd>
  <img src="media/StepLocation.png">
</kbd>

6. Copy the Initiation URL, this will be used for setting up an Alert Notification Channel in Grafana.
<kbd>
  <img src="media/InitiationURL.png">
</kbd>

6. Close the "Update Inbound Integration" and return to the main page of the Integration Builder. On this main page, at the bottom are shared libraries. Select or edit the Grafana Library.
7. Insert the API Key you generated in Grafana into `Grafana Token` constant, Which is accessible in the Flow Designer under Components>Constants. Reference [General Notes](#general-notes) section on how to generate the API key 
<kbd>
  <img src="media/GrafanaTokenConstant.png" height=300>
</kbd>


8. Add the Grafana Endpoint by clicking on Components>Endpoints in the Flow Designer. Add an endpoint and name it "Grafana". Add the URL to your Grafana instance. Make sure you save changes. 
<kbd>
  <img src="media/GrafanaEndPoint.png" height=500>
</kbd>

## Grafana set up
1. You first need to set up a notification channel in Grafana which can be found under the Alerting section
<kbd>
  <img src="media/CreateNotificationChannel.png" height=400>
</kbd>


2. Click on "New Channel" and create a new webhook found under "type". Name it, set Http Method to "POST", set URL as the URL you saved. **Reference step 6 in the xMatters set up for the URL**. Your channel should look something like this. **NOTE**: If you want to test out and see if the webhook works, you can click "Send Test" at the bottom.
<kbd>
  <img src="media/GrafanaChannel.png" height=400>
</kbd>


3. Go to the chart you want to be alerted on in Grafana, click "edit", click "Alert", then click "Notifications". Click the plus icon and add the Channel you just added in the previous step.
<kbd>
  <img src="media/AlertSectionGrafana.png" height=400>
</kbd>


## General Notes
* How to set up the Grafana API Key to plug into xMatters. **PLEASE NOTE: Grafana will only show the API you created ONCE. Suggestion is to copy and paste it in a notepad somewhere so you can get to it if you ever need it again**
<kbd>
  <img src="media/APIKeysGrafana.png" height=400>
</kbd>

* How to create API User in xMatters
Click "Users", click "Invite Users" or "Add Users". Information should be something like this.
<kbd>
  <img src="media/RESTAPIUser.png" height=500>
</kbd>
If it requires an email, the email can be something like email@xmatters.com 

# Testing
Do an action in your Grafana application or infrastructure that will trigger the alert conditions set up in the Alert. This will fire the webhook into the workflow and an event will be created, targeting the default recipients. After it targets the right person, you can use our 2-way integration by responding with "Pause Alert" to pause the alerting process in Grafana. Once you fix the issue in Grafana, you can come back to the original xMatters alert and use the response option "Resume Alert" to resume the alerting rule.
<kbd>
  <img src="media/GrafanaAlert1.png" height=500>
</kbd>

# Troubleshooting
If it doesn't work, then access the log to find out what's going wrong.

Click the Activity button in the upper right of the screen.

<kbd>
  <img src="media/Activity.png" height=400>
</kbd>

Select a flow element such as "Grafana Alert - Inbound from Grafana".

<kbd>
  <img src="media/ActivityAlert.png" height=400>
</kbd>

Select "Log" in order to view the log.

<kbd>
  <img src="media/ActivityLog.png" height=400>
</kbd>
