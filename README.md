# Simple CI/CD Pipeline

In this tutorial we are going to build a simple CI/CD pipeline using `Jenkins` as our `Continuous Integration` tool. Using `Jenkins` we're going to trigger a new build every time a change is being made to our `GitHub` Repository . By that, we will be able to build and test our software projects continuously, making it easier for developers to integrate changes to the project and making it easier for users to obtain a fresh build.

### Prerequisites

1. `Jenkins` [installed](https://www.jenkins.io/doc/book/installing/) and runs as a proccess using java on your machine
   - Plugins required:
     - Docker plugin
     - Git plugin
     - GitHub plugin
     - CloudBees Docker Build and Publish plugin 
2. `Docker` [installed](https://docs.docker.com/get-docker/) on our Jenkins host
3. Fork this project
4. `ngrok` [installed](https://ngrok.com/download)
5. An empty `Docker Hub` Repository

## Part I - Jenkins
1. In the left bar we will select "new item" and then "freestyle project"
<img src="images/Screenshot%20from%202021-05-17%2015-54-58.png" width="150" >
2. Under the `"source code management"` section we will paste our `GitHub` repo URL and Branches to build value will be `"*/main"`
<img src="images/Screenshot%20from%202021-05-17%2016-20-40.png" >
3. In the Build section we will add a build step `"Docker Build and Publish"` and fill it as shown below (using your private creds and Repository details) 
<img src="images/Screenshot%20from%202021-05-17%2016-23-53.png" >
4. Build triggers section as shown below
<img src="images/Screenshot%20from%202021-05-17%2016-31-47.png" width="200" >

## Part II - GitHub
Now that we finished with our `Jenkins` pipeline we need to go to our `GitHub` account and create a webhook that will trigger our `jenkins` job on every commit. Before that, we can't forget that our `Jenkins` runs on our local machine which means that we need to expose it to the outside world (`GitHub` cant send webhooks to local machines) and this is why we will use `ngrok`. `ngrok` will expose the http port of jenkins (by default - 8080) on our local machine to the outside world and will insure that our `Jenkins` server is able to get webhook triggers from `GitHub`.
* command to expose our jenkins server:
 ```bash
$  ngrok http 8080
```
<img src="images/Screenshot%20from%202021-05-17%2016-54-02.png" >



Now we will go to our `GitHub` account and create a webhook to our project.
we will set it like as the following:



<img src="images/Screenshot%20from%202021-05-17%2017-00-12.png" >

### Now lets check it all out!!

Commit a change on your `GitHub` Repository  and go to your `Jenkins` to check if a build has been triggered. 
<img src="images/Screenshot%20from%202021-05-17%2017-15-04.png" >


As you can see a job has been triggered and we have a new `Docker image` with the build number tag on our `Docker Hub` Repository:


<img src="images/Screenshot%20from%202021-05-17%2017-23-51.png" >

# WE HAVE MADE IT - we succesfully built a `CI` pipeline to our software project.
