# Simple Python Flask Dockerized Application - in progression - not done!#
In this tutorial we are going to build a simple CI-CD pipeline using `Jenkins` as our 'Continuous Integration' tool. Using 'Jenkins' we're going to trigger a new build every time a change is made to our 'GitHub' Repository . By that we will be able to build and test our software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build.
### Pre requirements
1. `Jenkins` [installed](https://www.jenkins.io/doc/book/installing/) and runs as a proccess using java on your machine
   - Plugins required:
     - Docker plugin
     - Git plugin
     - GitHub plugin
     - CloudBees Docker Build and Publish plugin 
2. `Docker` [installed](https://docs.docker.com/get-docker/) on our Jenkins host
3. Fork this project
4. 'ngrok' [installed](https://ngrok.com/download)

## Jenkins

















Build the image using the following command

```bash
$ docker build -t simple-flask-app:latest .
```

Run the Docker container using the command shown below.

```bash
$ docker run -d -p 5000:5000 simple-flask-app
```

The application will be accessible at http:127.0.0.1:5000 or if you are using boot2docker then first find ip address using `$ boot2docker ip` and the use the ip `http://<host_ip>:5000`
check
