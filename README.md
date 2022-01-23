# Kubeedge-Nodered-Docker

Project for running Node-RED in Docker


### Starting development Environment

docker run -p 1880:1880 -v ${PWD}/data:/data -e NODE_RED_ENABLE_PROJECTS=true --name kubeedge-nodered nodered/node-red

docker-compose up

Will start the development environtment including a mosquitto browser

The flows include a simple dashboard for processing incomming mqtt events.


### Health endpoints

When running containers within a managed cloud environment, it is often useful to provide some endpoints within the container, so the cloud management system can verify the container is still alive and responding to requests.

This project adds the Health Checking capability from [CloudNativeJS.io](https://www.cloudnativejs.io).  The integration has be done in the **server.js** file by adding the following lines of code:

```JavaScript
var health = require('@cloudnative/health-connect');

var healthcheck = new health.HealthChecker();
app.use('/live', health.LivenessEndpoint(healthcheck));
app.use('/ready', health.ReadinessEndpoint(healthcheck));
app.use('/health', health.HealthEndpoint(healthcheck));
```
