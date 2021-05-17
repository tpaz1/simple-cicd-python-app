# Simple CICD pipeline
In this tutorial we are going to build a simple CI-CD pipeline using `Jenkins` as our `Continuous Integration` tool. Using `Jenkins` we're going to trigger a new build every time a change is made to our `GitHub` Repository . By that we will be able to build and test our software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build.
### Pre requirements
1. `Jenkins` [installed](https://www.jenkins.io/doc/book/installing/) and runs as a proccess using java on your machine
   - Plugins required:
     - Docker plugin
     - Git plugin
     - GitHub plugin
     - CloudBees Docker Build and Publish plugin 
2. `Docker` [installed](https://docs.docker.com/get-docker/) on our Jenkins host
3. Fork this project
4. `ngrok` [installed](https://ngrok.com/download)
5. `Docker Hub` empty Repository

## Part I - Jenkins
1. In the left bar we will select "new item" and then "freestyle project"
<img src="images/Screenshot%20from%202021-05-17%2015-54-58.png" width="150" >
2. Under the "source code management" section we will paste our GitHub repo URL and Brances to build will be "*/main"
<img src="images/Screenshot%20from%202021-05-17%2016-20-40.png" >
3. In the Build section we will add a build step "Docker Build and Publish" and fill it as shown below (using your private cred and repository details) 
<img src="images/Screenshot%20from%202021-05-17%2016-23-53.png" >
4. Build triggers section as shown below
<img src="images/Screenshot%20from%202021-05-17%2016-31-47.png" width="200" >

## Part II - GitHub
Now that we finished with our `Jenkins` pipeline we need to go to our github account and create a webhook that will trigger our `jenkins` job on every commit, but before that we cant forget that our jenkins runs on our local machine which means that we need to expose it to the world (GitHub cant send webhooks to local machines) and for that we will use `ngrok`. `ngrok` will expose the http port of jenkins (by default - 8080) on our local machine to the world and will insure that our jenkins server is able to get webhook triggers from `GitHub`.
* command to expose our jenkins server:
 ```bash
$  ngrok http 8080
```
<img src="images/Screenshot%20from%202021-05-17%2016-54-02.png" >
Now we will go to our `GitHub` account and create a webhook to out project.
we will set it like that:
<img src="images/Screenshot%20from%202021-05-17%2017-00-12.png" >

### Now lets check it all out!!

Commit a change on your `GitHub` Repository  and go to your jenkins to check if a build has been triggerd. 
<img src="images/Screenshot%20from%202021-05-17%2017-15-04.png" >
As you can see a job has been triggerd.
And we have a new `Docker image` with the build number tag on our `Docker Hub` repository:
<img src="images/Screenshot%20from%202021-05-17%2017-23-51.png" >

# WE MADE IT - we succesfully built a `CI` pipeline to our software project.
