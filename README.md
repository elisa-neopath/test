# Node.js - Demo Web Application
This is a simple Node.js web app using the Express framework and EJS templates. It has been designed with cloud demos in mind, to show things like auto scaling in Azure and Application Insights monitoring

Based on the standard express-generator template with EJS views e.g. `express --git --view=ejs` but has been enhanced with Bootstrap, FontAwesome and App Insights.

The app has four basic pages accessed from the top navigation menu:
 - **INFO** - Will show some system & runtime information, and will also display if the app is running from within a Docker container.  
 - **WEATHER** - Gets the location of the client page (with HTML5 Geolocation). The resulting location is used to fetch a weather forecast from the [Dark Sky](http://darksky.net) weather API. The results are show using animated [Skycons](https://darkskyapp.github.io/skycons/). The has the added bonus of allowing you to see dependency calls (out to external APIs) when monitored by App Insights. Dark Sky API key needs to be provided, see configuration below
 - **CPU LOAD** - Simply runs a lot of maths calcs in a loop to max the CPU, can be used to trigger auto-scaling rules and other monitoring scenarios
 - **TODO** - This is a small todo/task-list app which uses MongoDB as a database. Enable this when demo'ing App Insights to show a more complete and real application. *Note.* this view only appears when configured, see configuration below
 
![screen](https://user-images.githubusercontent.com/14982936/43461431-674d705e-94cb-11e8-9633-00331d17c953.png)
![screen](https://user-images.githubusercontent.com/14982936/43461432-676b34f4-94cb-11e8-87cd-2abbf17a1c3d.png)
![screen](https://user-images.githubusercontent.com/14982936/43461433-6785cea4-94cb-11e8-99a6-3359f296ba3f.png)


## Running 
Standard `npm install` and start with `npm start`. Web app will be listening on the usual Express port of 3000 or what is set in `PORT` environmental variable. Tested with both Node 6.11 and 8.9


## Configuration 
The following configuration environmental variables are used. These can be set directly or will be picked up from an `.env` file if it is present.

|Name|Default|Description                   |
|----|-------|------------------------------|
|PORT|4000   |Port the server will listen on|
|MONGO_CONNSTR|*none*   |Connect to specified MongoDB connection string, when set the Todo feature will be enabled in the menu bar|
|APPINSIGHTS_INSTRUMENTATIONKEY|*none*    |Enable Application Insights monitoring|
|WEATHER_API_KEY|*none*    |DarkSky weather API key. [Info here](https://darksky.net/dev)|


## Docker 
Public Docker image is [available on Dockerhub](https://hub.docker.com/r/bencuk/nodejs-demoapp/).  
Note. The Docker image includes SSH support, this is to enable the web console feature when running this app as a container in Azure Web App for Containers.  
Run with `docker run -d -p 3000:3000 bencuk/nodejs-demoapp`


## Application Insights 
The app has been instrumented with the Application Insights SDK, it will however need to be configured to point to your App Insights instance.  
To configure this, set the `APPINSIGHTS_INSTRUMENTATIONKEY` environmental variable to the relevant key for your active instance. If running in an Azure Web App, this can be set as an application setting in Azure.

[This article](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-nodejs) has more information on monitoring App Insights with Node.js 

## Azure Templates
Templates for deployment to Azure with "quick deploy" buttons are [here](azure-deploy/)

## Updates
* Dec 2018 - Modified weather to use client browser location, rather than use IP
* Jul 2018 - Switched todo app over to MongoDB, fixed weather
* Feb 2018 - Updated App Insights monitoring
* Nov 2017 - Update to use Node 8.9
* Oct 2017 - Updated App Insights, improved Dockerfile
* Sept 2017 - Added weather page
* Sept 2017 - Major revamp. Switched to EJS, added Bootstrap and App Insights
* Aug 2017 - Minor changes and fixes for CRLF stuff
* July 2017 - Updated Dockerfile to use super tiny Alpine Node 6 image
* June 2017 - Moved repo to Github

#test
