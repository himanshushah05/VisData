# VisData
VisData is a data monitoring project, where sensor data can be monitored and visualised. 

## Description:
The project includes an ESP32 connected to DHT11 sensor. The data is written to google sheets using [IFTTT](https://ifttt.com/explore). The google sheets data is further visualized using [Grafana](https://grafana.com/) dashboard.

## Hardware Setup
- The hardware is very simple. It includes just a DHT11 sensor connected to ESP32. 
- Connections - signal pin connected to D4 of ESP32

## Software 
### 1. Setting up IFTTT applet:
- Create a new applet after logging in to the [IFTTT](https://ifttt.com/explore).
- In the _If this_ place, select ___Webhooks___ and choose ___Receive a web request___ as the _trigger_. 
- Name the event as per your choice. (In my case, it is dht_readings)
- In the _then that_ place, select ___Google Sheets___ as the _service_.  
- Connect the ___Google Sheets___ service with your Google sheets and then choose the _action_ as ___add row to spreadsheet___  
- Then, complete the action fields. Give the spreadsheet a name, leave the _Formatted row_ field as default, and then, choose a Google Drive folder path. (If you leave this field empty, IFTTT will create a folder called “IFTTT” in your Google Drive folder to save the spreadsheet)
- Finally, click the __Create action__ button.
#### Testing the applet
- Go to [Webhooks Service Page](https://ifttt.com/maker_webhooks) and go to __Documentation__.
- The page will show your unique ___API key___. (Save this for later use)
- Fill the _trigger event_ section with your event name.
- Then fill some values in the JSON body to send test it. (IFTTT supports 3 values only, if you want to add more, you can fill a json with multiple data and then seperate it in google sheets to different column)
- Click ___test it___ button and it will show you a green message saying “Event has been triggered”.
- Go to your drive and search for IFTTT, in that folder the new spreadsheet will be there and it will have the reading that just you added while testing.

### 2. Creating Grafana Dashboard
- Sign up to [Grafana](https://grafana.com/).
- After downloading Grafana from _Downloads_, visit [http://localhost:3000/](http://localhost:3000/). It will load the Grafana.
- The Grafana can take data from different sources so in order to setup Google sheets as the data source, we have to install plugin for it.
- Go to [https://grafana.com/grafana/plugins/grafana-googlesheets-datasource/?tab=installation](https://grafana.com/grafana/plugins/grafana-googlesheets-datasource/?tab=installation) and install the plugin.  
- Now, go to the Grafana (i.e., [http://localhost:3000/](http://localhost:3000/) )and under use as data source, search for google sheets plugin and select it. 


