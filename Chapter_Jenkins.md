#### Need of Jenkins
Want to get notifications instantly when your code broke? Need some tool to integrate automation for your application or software? Has wide range of plugins to support your build, test and deployment process? Easy to configure and Free?Solution: Jenkins.

#### Nah, explain further.

![Traditional Software Delivery Process](https://cdn.hashnode.com/res/hashnode/image/upload/v1643820828086/51SRh_LMhZ.png)

Above shown is a raw process on how development cycle worked traditionally. Consider your team working on a new functionality for an application and you want to have it deployed to the upcoming release version. Initially you push your code to a version control system like Github, BitBucket or your company's private VC system. All the manual work ends here. Now starts the integration and delivery.
The problem here is the build process takes a considerable amount of time, in fact development teams had a custom nightly build convention where all the build process were scheduled at night, but 'nightly' build was relative of different time-zones. Lets say, a company decides for night build of 12:30AM EST, the build would be 10:30AM IST and 4:00PM AEST and therefore all developers had to commit their code for build at their respective timezones which affected productivity of developers in IST and AEST region as they had to wait till the build and test was completed.
Also if the code broke and the tests failed were no ascertain means to pick-point which team or particularly who wrote that piece of code.

#### So?
Jenkins is an open-source versatile automation server completely built in Java, for integrating the workflow of building, testing and deploying a software. Jenkins transitioned the traditional software delivery cycle to a fast, extensive and customisable CI/CD process. With the help of Jenkins its possible to-

1. Get instant build notifications every-time code is pushed to the repository.
2. Test the built code on wide range of test combinations for achieving maximum test-coverage and statistical data on how the code performed for each test-input.
3. Get instant result notifications after every test-session.
4. Create roles for each responsibility and manage what to hide for each role on what they could read and/or write to.
5. Build your own automation tools using wide range of plugins available at https://plugins.jenkins.io

This is how Jenkins helped in rejuvenating to a frictionless CI/CD process.

![New Software Delivery Process](https://cdn.hashnode.com/res/hashnode/image/upload/v1643820645462/kI5vLRmRA.png)

#### Installing Jenkins
To install Jenkins on your local setup read [Jenkins official download guide](https://www.jenkins.io/download/)

##### Installing Jenkins as a container inside Docker.
To install Jenkins as a container from Jenkins Docker image, execute-
`docker pull jenkins/jenkins:lts-jdk11`

#### Jenkins Model
Here's a high level view of Jenkins application

![Jenkins Model](https://cdn.hashnode.com/res/hashnode/image/upload/v1643804112483/zvV-b8Ma4.png)

#### Components of Jenkins
- Plugins
- Jenkins Pipeline
- JenkinsFile

#### Plugins
A Plugin is an extension tool to help streamline the process of building, testing or deploying a software. There are more than 1800 plugins available built for frictionless development such as analysing or testing the codebase, sending custom notifications of test or build results to developers, integrate Git with Jenkins and many more.   We can install more than one plugins on top of our Jenkins local environment to implement these different functionalities that increases the efficacy of CI/CD process. These plugins are built by awesome developers of Jenkins Open-source community and you can browse all these plugins and their information on [Jenkins Plugins Website](https://plugins.jenkins.io/).

Few examples of plugins are-
GitHub Groovy Library, GitHub Branch Source Plugin, SSH Build Agents, LDAP, Credentials Binding Plugin, OWASP Markup Formatter, PAM Authentication.

Plugins can be installed using 2 ways-

- **"Plugin Manager" in the web User Interface. **
![Manage Plugin through Web UI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oagvx6ggyuq380gb1zlk.png)

- **Jenkins Command Line Interface.**

```
java -jar jenkins-cli.jar -s http://localhost:8080/ install-plugin SOURCE ... [-deploy] [-name VAL] [-restart]
``` 
Installs a plugin either from a file, an URL, or from update center.

SOURCE: If this points to a local file, that file will be installed. If
             this is an URL, Jenkins downloads the URL and installs that as a
             plugin.Otherwise the name is assumed to be the short name of the
             plugin in the existing update center (like "findbugs"),and the
             plugin will be installed from the update center.

 -deploy: Deploy plugins right away without postponing them until the reboot.

 -name VAL : If specified, the plugin will be installed as this short name
             (whereas normally the name is inferred from the source name
             automatically).

 -restart  : Restart Jenkins upon successful installation.

#### Jenkins Pipeline
Jenkins Pipeline is structured set of plugins, required for integration of your software, declared inside a file called JenkinsFile.

#### JenkinsFile
To define the software delivery pipeline we need to write the steps inside a text file called `JenkinsFile`. Every software using Jenkins is required to define JenkinsFile inside its project repository.

![JenkinsFile](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tiqyrk40m7o6skykucnz.png)

We can build your Pipeline's JenkinsFile through either-


- Jenkins User Interface

![Jenkins User Interface](https://cdn.hashnode.com/res/hashnode/image/upload/v1643806568720/qyFHQa9rj.png)
 
 or
- BlueOcean User Interface 

![BlueOcean User Interface ](https://cdn.hashnode.com/res/hashnode/image/upload/v1643806377667/DCLcMwY6i.png)
 
or
- Using Source Code Management (SCM)

![Using Source Code Management (SCM)](https://cdn.hashnode.com/res/hashnode/image/upload/v1643807322190/JXZBsLRTXw.png)

And to code the JenkinsFile we can use either of the two syntaxes:

1. Scripted Pipeline(must be written in [Groovy ](http://groovy-lang.org/semantics.html))
2. Declarative Pipeline

- **Scripted Pipeline:**
These pipelines are initiated with the directive `node`.
Here's an example structure of Scripted Pipeline-

```
node{
    stage('Build'){
        try{
        }
        catch(e){
        }
    }
    stage('Test'){
        if(condition){
        }
        else{
        }
    }
    stage('Deploy'){
    }
}
```

- **Declarative Pipeline:**
These pipelines are initiated with syntax `pipeline`
Here's an example structure of a combination of: parallel and non-parallel declarative pipeline.

```
pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
            }
        }
        stage('TestAndDeploy'){
            parallel{
                stage('Test'){
                    steps{
                    }
                }
                stage('Deploy'){
                    steps{
                    }
                }
            }
        }
    }
}
```
in the above pipeline stage('Build') is executed first and stages: stage('Test') & stage('Deploy') are run in parallel because of the `parallel` directive.

Just like the `parallel` keyword there are many others available for their discrete functionalities, these keywords are called Directives; a few to mention are:

- `when` - It allows the Pipeline to decide whether the stage should be executed a depending on the given condition.
Example: `when{ branch main}`
- `stage` - This directive can comprise of one or more directives collectively used to define-build a particular process of development cycle. 
Example: `stage('Test'){...}` the stage 'Test' would consist of set of instructions that would trigger every time any code is being sent for testing.
- `tools` - It is used to define tools to auto-install for Jenkins server.



#### Alternative to Jenkins
CircleCI
