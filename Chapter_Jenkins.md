Want to get notifications instantly when your code broke? Need some tool to integrate automation for your application or software? Need wide range of plugins to support your build, test and deployment process? Easy to configure and Free? And have an amazing community around itself? Solution: Jenkins.

### Why is Jenkins needed?

![Traditional Software Delivery Process](https://cdn.hashnode.com/res/hashnode/image/upload/v1644314049515/mQ0-KP8TZ.png)
Above diagram depicts a raw process on how development cycle worked traditionally. Consider your team working on a new functionality for an application and you want to have it deployed to the upcoming release version. Initially you push your code to a Version Control system like Github, BitBucket or your company's private VC system. All the manual work ends here. 

Now starts the integration and delivery process. The problem here is that the build process takes a considerable amount of time to build your software. Therefore the development teams had a custom nightly build convention where all the build process were scheduled at night, but "nightly" build is relative to different time-zones. Let's say, a company decides for night build at 12:30AM EST, but that build would be 10:30AM IST and 4:00PM AEST and hence all IST and AEST developers would have to commit their code for build during their work timezones which affected their productivity. Also the tests cases were limited and did not have wide coverage. So you would have to wait till your code was built and pushed to the test server to check if it passed the predefined tests, and if the tests and build failed the source-code was pushed back to your team.

 In the whole process if the code broke and the tests failed there were no ascertain means to pick-point which team or particularly who wrote that piece of code. 

As we observe here, this whole process is definitely not an optimal way to your deliver your software and making it production ready.

### Jenkins
Jenkins is an open-source versatile automation server completely built in Java, for integrating the workflow of building, testing and deploying a software. Jenkins transitioned the traditional software delivery cycle to a fast, extensive and customisable CI/CD process. With the help of Jenkins its possible to-

1. Get instant build notifications every-time your code is pushed from the repository to build.
2. Parallel Build i.e run more than one build processes in parallel to reduce your build time.
2. Test the built code on wide range of test combinations for achieving maximum test-coverage and statistical data on how the code performed for each test-input.
3. Get instant result notifications after every test-session.
4. Create roles for each responsibility and manage what to hide for each role on what they could read and/or write to.
5. Build your own set of integration tools using wide range of plugins available at https://plugins.jenkins.io

> Fun Fact:  We can integrate Jenkins with some popular cloud platforms including AWS, VMWare, Google Cloud Platform, Azure,  IBM Cloud, Digital Ocean etc.

This is how Jenkins helped in rejuvenating to a frictionless CI/CD process.

![Software Delivery Process using Jenkins](https://cdn.hashnode.com/res/hashnode/image/upload/v1644314092880/IqeJpCUg7.png)

### Installing Jenkins
To install Jenkins on your local setup read [Jenkins official download guide](https://www.jenkins.io/download/)

#### Installing Jenkins as a container inside Docker.
To install Jenkins as a container from Jenkins Docker image, execute-
`docker pull jenkins/jenkins:lts-jdk11`

### Architecture of Jenkins Model
Here's a high level view of Jenkins application

![Jenkins Model](https://cdn.hashnode.com/res/hashnode/image/upload/v1643804112483/zvV-b8Ma4.png)

#### Components of Jenkins
- Plugins
- Jenkins Pipeline
- JenkinsFile

### Plugins
A Plugin is an extension tool to help streamline the process of building, testing or deploying a software. There are 1800+ plugins available built for integrating purpose such as analysing or testing the codebase, sending custom notifications of test or build results to developers, integrate Git with Jenkins and many more. We can install more than one plugins on top of our Jenkins local environment to implement these different functionalities that increases the efficacy of CI/CD process. These plugins are built by awesome developers of Jenkins Open-source community and you can browse all these plugins and their information on [Jenkins Plugins Website](https://plugins.jenkins.io/).

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

- `SOURCE`: If this points to a local file, that file will be installed. If this is an URL, Jenkins downloads the URL and installs that as a plugin.
- `-deploy`: Deploy plugins right away without postponing them until the reboot.
- `-name VAL` : If specified, the plugin will be installed as this short name (whereas normally the name is inferred from the source name automatically).
- `-restart`  : Restart Jenkins upon successful installation.

### Jenkins Pipeline
Jenkins Pipeline is structured set of plugins, required for integration of your software, declared inside a file called JenkinsFile.

### JenkinsFile
To define a Jenkins pipeline we need to write a set of steps inside a text file called `JenkinsFile`.Thus JenkinsFile implements "Pipeline as a Code". Every software using Jenkins is required to define JenkinsFile inside its project repository. 

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

1. Scripted Pipeline(should be written in [Groovy ](http://groovy-lang.org/semantics.html), is flexible but have steep learning curve)
2. Declarative Pipeline(recently added feature, easy to learn but not so powerful/flexible)

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

Just like the `parallel` keyword there are many others available each having their discrete functionalities, these keywords are called Directives; a few to mention are:

- `when` - It allows the Pipeline to decide whether the stage should be executed a depending on the given condition.
Example: `when{ branch main}`
- `stage` - This directive can comprise of one or more directives collectively used to define-build a particular process of development cycle. 
Example: `stage('Test'){...}` the stage 'Test' would consist of set of instructions that would trigger every time any code is being sent for testing.
- `tools` - It is used to define tools to auto-install for Jenkins server.

---

### Wrap Up
#### Alternative to Jenkins 
Here are few other CI/CD tool options to Jenkins with each having its own advantages and disadvantages:
- CircleCI
- GitLab
- Travis CI 

`Reference`: Jenkins Documentation

#### What next?
Now that you are aware of Jenkins as a next step you might need to containerise your application. Containerising your application helps in shipping your application to different systems without worrying about dependencies, scaling and even deploying your application faster. I have made a detailed "Guide to Docker" so check that out!

Thank you for taking time to read my article :)

#### Do connect with me on- 
[Twitter](https://twitter.com/atharvashinde_), 
[GitHub](https://github.com/Atharva-Shinde), and
[LinkedIn](https://www.linkedin.com/in/atharva-shinde-6468b4205/)
