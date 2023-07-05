# 🌤➡🖥 VisData
VisData is a data monitoring project, where sensor data can be monitored and visualised. 

## 🗒 Description:
The project includes an ESP32 connected to DHT11 sensor. After every 15 minutes, my system wakes up from deep sleep and records the reading and goes to deep sleep again. The data is written to google sheets using [IFTTT](https://ifttt.com/explore). The google sheets data is further visualized using [Grafana](https://grafana.com/) dashboard.

## 📸 Images of IFTTT applet and Grafana Dashboard
### Dashboard 
![](https://github.com/himanshushah05/VisData/blob/main/dashboard%20gif.gif)

### IFTTT Applet
<img src="https://github.com/himanshushah05/VisData/blob/main/Applet%20image.png" width = 20% height=10% />

## 🔧 Hardware Setup
- The hardware is very simple. It includes just a DHT11 sensor connected to ESP32. 
- Connections - signal pin connected to D4 of ESP32

## 🖥 Software 
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

#### Changes in Arduino code as per the applet
- Replace your wifi credentials in the code
- Put your resource URL as "/trigger/__{your_event_name}__/with/key/gJ868-fZ2z0QHxAW9vAlngrMRAcrFVnNElyAwuOxh8S"
- My system is deep sleep mode for the whole time and wakes up only once in every 15 minutes hence saving battery. You can change this value by changing `TIME_TO_SLEEP` variable to as many seconds you want. 

### 2. Creating Grafana Dashboard
#### Adding the Google Sheets Plugin
- Sign up to [Grafana](https://grafana.com/).
- After downloading Grafana from _Downloads_, visit [http://localhost:3000/](http://localhost:3000/). It will load the Grafana.
- The Grafana can take data from different sources so in order to setup Google sheets as the data source, we have to install plugin for it.
- Go to [https://grafana.com/grafana/plugins/grafana-googlesheets-datasource/?tab=installation](https://grafana.com/grafana/plugins/grafana-googlesheets-datasource/?tab=installation) and install the plugin.  
- Now, go to the Grafana (i.e., [http://localhost:3000/](http://localhost:3000/) )and under add data source, search for google sheets plugin and select it.
- To configure the data source, select __API key__ as the Auth. (Make a note that this API key is different from the IFTTT API key)
- Now to generate API key for authentication of google sheets, go to [https://console.cloud.google.com/home/](https://console.cloud.google.com/home/)
- Create new project and under API & services, go to credentials and generate a new API key. 
  Now go to the dashboard from the same menu and click on __Enable API and Services__, search for __Google Sheets API__ and enable it.
- Now copy paste this Google cloud API key into Grafana and click save and test.          

Now, Let's create the Dashboard

#### 👨‍💻 Creating Dashboard
- Now, in the Grafana menu, go to Dashboard and create a new dashboard.
- then Add new Visualization and then select data source as Google Sheets and then under spreadsheet ID enter the part of url from d/{ID}/edit.
for eg, https://docs.google.com/spreadsheets/d/1WolxfNRQPFwx5RC2aLBHSdERplVnZVVL1kQcOXznY64/edit?usp=sharing
in this link 1WolxfNRQPFwx5RC2aLBHSdERplVnZVVL1kQcOXznY64 will be the ID.
- Then by using different Visualization tools such as Gauges, graphs and tables, We can visualize the data as per our requirement.




