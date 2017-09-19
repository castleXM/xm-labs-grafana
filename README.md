# Grafana
Grafana is an open source metric analytics & visualization suite. It is most commonly used for visualizing time series data for infrastructure and application analytics but many use it in other domains including industrial sensors, home automation, weather, and process control. This integration extends the ability to alert the person on call to a group and pause or unpause an alert coming out of Grafana using out closed-loop integration. Check out the sweet video [here](https://youtu.be/Dj2sEaZzXi0).

# Pre-Requisites
* [Grafana](https://grafana.com/) version 4.4.3
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [GrafanaAlert.zip](GrafanaAlert.zip) - Communication Plan containing the Inbound and Outbound integration with form templates

# How it works
An alert fires a webhook to the xMatters integration builder. The integration builder parses the incoming JSON and builds the event, then fires the event to notify the default recipients. Alternatively [subscriptions](http://help.xmatters.com/OnDemand/userguide/receivingalerts/subscriptions/howtousesubscriptions.htm) can be set up to notify the desired parties. From the alert, you can pause the alert in Grafana to investigate the issue. When the issue is fixed, you can resume the alerting rule.  

# Installation

## xMatters set up
1. Login as the integration user in xMatters and navigate to the Developer Tab.(NOTE: Make sure the integration user has **REST Web Services User** Role.
2. Import the [GrafanaAlert.zip](GrafanaAlert.zip) Steps to import a communication plan: [Here]( http://help.xmatters.com/OnDemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)
3. Enable the plan, click Edit and get into the "Integration Builder"
4. Click into the Inbound integration labeled "Inbound from Grafana" and navigate to the Script Editor on Step 5
5. Insert your group recipient(s) where it says [INSERT GROUPS HERE]. 
<kbd>
  <img src="InsertGroupHere.png">
</kbd>

6. Save and return to the previous page. Click on "Update Inbound Integration" and copy the URL to have it handy later.
<kbd>
  <img src="xMattersURL.png">
</kbd>

7. Follow the bread crumb back to the integration builder in for "Grafana Alert" and click on the "Shared Libraries" and click on Grafana.
8. Insert the API Key you generated in Grafana into the code.







## Grafana set up
Any specific steps for setting up the target application? The more precise you can be, the better!

Images are encouraged. Adding them is as easy as:
```
<kbd>
  <img src="media/cat-tax.png" width="200" height="400">
</kbd>
```

<kbd>
  <img src="media/cat-tax.png" width="200" height="400">
</kbd>


# Testing
Be specific. What should happen to make sure this code works? What would a user expect to see? 

# Troubleshooting
Optional section for how to troubleshoot. Especially anything in the source application that an xMatters developer might not know about, or specific areas in xMatters to look for details - like the Activity Stream? 
