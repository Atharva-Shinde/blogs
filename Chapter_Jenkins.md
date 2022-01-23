#### Need of Jenkins
Want to get notifications instantly when your code broke? Need some tool to integrate automation for your application or software? Has wide range of plugins to support your build, test and deployment process? Easy to configure and Free?Solution: Jenkins.

#### Nah, explain further.


![Traditional Software Delivery Process](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3atmzuca89609i07a7h5.png)

Above is a raw process on how development cycle worked traditionally. Consider your team working on a new functionality for an application and you want to have it deployed to the upcoming release version. Initially you push your code to a version control system like Github, BitBucket or your company's private VC system. All the manual work ends here. Now starts the integration and delivery.
The problem here is the build process takes a considerable amount of time, in fact development teams had a custom nightly build convention where all the build process were scheduled at night, but 'nightly' build was relative of different time-zones. Lets say, a company decides for night build of 12:30AM EST, the build would be 10:30AM IST and 4:00PM AEST and therefore all developers had to commit their code for build at their respective timezones which affected productivity of developers in IST and AEST region as they had to wait till the build and test was completed.
Also if the code broke and the tests failed were no ascertain means to pick-point which team or particularly who wrote that piece of code.

#### So?
Jenkins is a versatile automation server for building, testing and deploying software developed in Java. Jenkins transitioned the traditional software delivery cycle to a fast, extensive and customisable CI/CD process.


#### Jenkins Architecture


#### Installing Jenkins
to install Jenkins on your local setup read [Jenkins official download guide](https://www.jenkins.io/download/)

##### Installing Jenkins as a container
To install Jenkins as a container from Jenkins Docker image execute-
`docker pull jenkins/jenkins:lts-jdk11`

#### Jenkins Pipeline
Jenkins Pipeline is a collective of plugins which supports tools for implementing 

#### Alternative to Jenkins
CircleCI
