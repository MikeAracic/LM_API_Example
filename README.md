# LM_API_Example
 ©LogicMonitor, Inc. 2015

## DMV wait time 
 Python script dmvtimes is a python script that uses the [LogicMonitor API](http://help.logicmonitor.com/developers-guide/api-quick-start/) to poll a datapoint for data, and then outputs either a color or one of the [blink(1)](https://blink1.thingm.com/) default patterns. The script is actually called in by the blink(1) software itself. It demonstrates one way to retrieve a datapoint from the json returned by the LogicMonitor API.
## NOC Blink
Python script noc_blink and its supporting module(s) connect to a LogicMonitor environment and produce a summary of active alerts. They dynamically convert that alert information into a pattern of blinks for the blink(1) in order to serve as a hands-off status indicator. If there's a collector that's down and the alert hasn't been acknowledged and the collector is not in a scheduled downtime, the pattern will begin with a bright white SOS. If there are Acknowledged alerts, critical alerts, errors, or warnings, active, it will count them up and produce short flashes for 1-10, medium flashes for tens betwen 11-100, and long flashes for every hundred when there are more. (rounding up at 5 and 50 respectively) It uploads the pattern using the blink light's API, then passes the name of the pattern back to the blink(1) software to start the blinking. There's an [official python API](https://github.com/todbot/blink1/tree/master/python), but I couldn't get it to work properly, so I worked around it.

Installation/Configuration:

1. Verify that python and the requests module are installed on whichever system you choose to run this.

2. Install the blink(1) software and test to make sure that the device.

3. In the blink(1) advanced preferences screen, select "start API server" and restart the blink(1) software.

4. In LogicMonitor, [create a read-only user](http://help.logicmonitor.com/getting-started/i-just-signed-up-for-logicmonitor-now-what/10-adding-users-and-roles/). If you use any special characters, be prepared to URL encode them ([see LogicMonitor's page about authentication](http://help.logicmonitor.com/developers-guide/authenticating-requests/))

5. [Install](http://docs.python-requests.org/en/latest/user/install/) the python requests package.

6. Download the contents of the repository into a directory

7. Edit file noc_blink, and set the company, user, and password assignments to match the name of your environment, and the user and password that you set up in step 4 respectively.

8. Set the noc_blink file as executable

9. In the blink(1) application, under tools, add the location of the noc_blink script as type "script" and set it to run at once a minute (or longer) You should see evidence that it's running the script and see lights if there are active alerts or down collectors in your environment.

Errata/ToDo
 * Alert totals do not currently reflect the presence or absence of applicable scheduled downtime
 * Better/more reusable data model
 * Multiple blink control (would probably require a different approach to starting the pattern)
 * Phillips Hue maybe?
 
 
 
 Both require and use the ["Requests"](http://docs.python-requests.org/en/latest/) module as a prerequisite.
 
