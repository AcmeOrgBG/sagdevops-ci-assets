# sagdevops-ci-assets
Software AG DevOps library to support assets CI (continuous integration) with webMethods 9.x and 10.0. Works together with [webMethods sample project layout](https://github.com/SoftwareAG/webmethods-sample-project-layout)


## Description
sagdevops-ci-assets is a library that easily enables CI for your webMethods projects. You can setup your infrastructure in minutes and then deploy flowlessly on your test service while also checking the quality
by running all tests uploaded your version control.


## Set-up

### webMethods Installation
Prepare your webMethods installation - your build server can contain only a plain IntegrationServer with Deployer. Keep the server plain - there is no need for designer or database connection.
Your test server can be more complex as CI will execute unit and integration tests against it. The build and the test server must reach each other over http so that the deployment and the testing can be performed.

### CI Library
Download the library on your build server by

```
git clone https://github.com/SoftwareAG/sagdevops-ci-assets.git
```

Edit the _System.properties_ to correspond to your inftrastucture - deployerHost is the machine where your Deployer is running(normally the build server) where targetHost is your test server - where the packages will be deployed and tested. 

*Notice* change the path the Deployer if you're not using the _default_ Integration Server instance.



### Jenkins Pipeline Job
In Jenkins, create a new item from type pipeline. Give it a **unique name** as we use the job name as identifier further down the process. Scroll down the page to the pipeline definition
and choose _Pipeline definition from SCM_. Choose git as system and give the url of the webmethods-sample-project-layout - _https://github.com/SoftwareAG/webmethods-sample-project-layout.git_

This sample project contains two pre-created pipeline definitions - Jenkinsfile.win and Jenkinsfile.unix that run on the respective operating systems. Type in the correct file in respect of you 
build server OS.

Those pipeline definition are orchestrating all steps around the build, deploy and the test on your server. If the all environment variables are set correctly you should not change anything here.


## How it works
After your pipeline job is set-up, trigger it. It will download the pipeline description automatically, then checkout the sources, build the core, deploy the code and run tests. 
Whenever a developer checks in new IS packages and Tests those will be automatically deployed and all new tests will be executed. For this to work, the structure defined here  _https://github.com/SoftwareAG/webmethods-sample-project-layout.git_ has followed.

## Notice
The wM Test Suite tests will have to be places in a directory a *setup* directory inside the test project, so that it can be picked up by the test executor.
_____________
Contact us at [TECHcommunity](mailto:technologycommunity@softwareag.com?subject=Github/SoftwareAG) if you have any questions.












