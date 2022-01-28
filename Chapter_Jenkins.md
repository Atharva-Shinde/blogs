#### Need of Jenkins
Want to get notifications instantly when your code broke? Need some tool to integrate automation for your application or software? Has wide range of plugins to support your build, test and deployment process? Easy to configure and Free?Solution: Jenkins.

#### Nah, explain further.


![Traditional Software Delivery Process](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3atmzuca89609i07a7h5.png)

Above shown is a raw process on how development cycle worked traditionally. Consider your team working on a new functionality for an application and you want to have it deployed to the upcoming release version. Initially you push your code to a version control system like Github, BitBucket or your company's private VC system. All the manual work ends here. Now starts the integration and delivery.
The problem here is the build process takes a considerable amount of time, in fact development teams had a custom nightly build convention where all the build process were scheduled at night, but 'nightly' build was relative of different time-zones. Lets say, a company decides for night build of 12:30AM EST, the build would be 10:30AM IST and 4:00PM AEST and therefore all developers had to commit their code for build at their respective timezones which affected productivity of developers in IST and AEST region as they had to wait till the build and test was completed.
Also if the code broke and the tests failed were no ascertain means to pick-point which team or particularly who wrote that piece of code.

#### So?
Jenkins is a versatile automation server developed completely in Java for automating the workflow of building, testing and deploying software. Jenkins transitioned the traditional software delivery cycle to a fast, extensive and customisable CI/CD process. Using Jenkins its possible to

1. Get instant build notifications every-time code is pushed to the repository.
2. Test the built code on wide range of test combinations for achieving maximum test-coverage and statistical data on how the code performed for each test-input.
3. Get instant result notifications after every test-session.
4. Create roles for each responsibility and manage what to hide from users and what they could read and/or write to.
5. Build your own automation tools using wide range of plugins available at https://plugins.jenkins.io

Few examples of plugins-
GitHub Groovy Library, GitHub Branch Source Plugin, SSH Build Agents, LDAP, Credentials Binding Plugin, OWASP Markup Formatter, Ant, Gradle, PAM Authentication.


#### Jenkins Architecture


#### Installing Jenkins
to install Jenkins on your local setup read [Jenkins official download guide](https://www.jenkins.io/download/)

##### Installing Jenkins as a container
To install Jenkins as a container from Jenkins Docker image execute-
`docker pull jenkins/jenkins:lts-jdk11`


#### Jenkins Pipeline
Jenkins Pipeline is a collective of plugins for creating declarative automations. 

#### JenkinsFile
To define an automated process for our Jenkins Pipeline we need write the steps inside a text file called `JenkinsFile`.

![JenkinsFile](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tiqyrk40m7o6skykucnz.png)

We can create a pipeline's JenkinsFile inside Jenkins User Interface or using Source Code Management, with either of the two syntaxes:

1. Scripted Pipeline(mostly used)
2. Declarative Pipeline(relatively new)


- 
Scripted Pipeline:
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

- 
Declarative Pipeline:
These pipelines are initiated with syntax `pipeline`
Here's an example structure of a mix: parallel and non-parallel declarative pipeline.

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
