# Build Automation & CI/CD with Jenkins

### Demo Project:
CD - Deploy Application from Jenkins Pipeline to EC2 Instance (automatically with docker)

### Technologies Used:
AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

### Project Objectives:
- Prepare AWS EC2 Instance for deployment (Install Docker)
- Create ssh key credentials for EC2 server on Jenkins
- Extend the previous CI pipeline with deploy step to ssh into the remote EC2 instance and deploy newly built image from Jenkins server
- Configure security group on EC2 Instance to allow access to our web application

### Configure and EC2 Instance and Install Docker
1. follow the setup in the first two sections from the previous demo above

### Create ssh key credentials for EC2 server on Jenkins
1. install SSH Agent plugin in Jenkins
2. create ssh key credentials for the .pem file
    - in the multibranch pipeline, create credentials only for this pipeline's scope
    - click 'Credentials' from the menu and click the store for the specific pipeline and create credentials
    - select 'SSH Username with private key'
        - enter an id
        - enter 'ubuntu' for username
        - copy and paste the content of the .pem file
3. use the credentials in the jenkinsfile for connecting to the ec2 remote server
    - go to 'Pipeline Syntax' in the side menu of your pipeline, you can generate a script for using SSH Agent
    - scroll to 'Steps' section and select 'sshagent: SSH Agent' and select your credentials
    - click 'Generate Pipeline Script' and it will generate a sample script for you to use in the jenkinsfile
4. update the jenkinsfile, add the sshagent syntax in the deploy step

### Extend the previous CI pipeline for java-maven-app with a deploy step
1. add a deploy stage to the CI pipeline in the jenkinsfile
    - this step will ssh into the ec2 server and deploy the docker image that was pushed to the dockerhub repository
```
stage('deploy') {
    steps {
        script {
            echo 'deploying docker image to EC2...'
            def dockerCmd = "docker run -p 3080:8080 -d ${IMAGE_NAME}"
            sshagent(['ec2-server-key']) {
                // -o StrictHostKeyChecking=no, suppresses popup when connecting to the ec2 server
                sh "ssh -o StrictHostKeyChecking=no ubuntu@<ec2-server-ip> ${dockerCmd}"
                // make sure to do 'docker login' on the ec2 server if needed
            }
        }
    }
}
```
- Jenkinsfile : https://github.com/KajalLad1206/java-maven-app-multipipe/blob/app-deploy/Jenkinsfile
  
5. change in code,commit and git push it will trigger in github and deploy stage execute 
    - in your browser :public_ip_of_server/project name
    ex. http://35.182.166.224:3080/myproject

---
### Demo Project:
Configure Webhook to trigger CI Pipeline automatically on git push

### Technologies Used:
Jenkins, GitHub, Git, Docker, Java, Maven

### Project Objectives:
- Configure Jenkins to trigger the CI pipeline, whenever a change is pushed to GitHub
  
### Configure Jenkins to Automatically Trigger the CI Pipeline
-  if using GitHub
    - in the Configure settings of your Pipeline job, select 'hook trigger for GITScm Polling' in the 'Build Triggers' section
    - in the GitHub repo for your project, go to 'Settings'
        - go to 'Webhooks' > 'Add Webhook'
        - Payload URL = Jenkins URL + '/github-webhook/'
                ex : http://35.182.166.224:8080/github-webhook/
        - Content Type = application/json
        - Secret = optional
        - Which events? = Just the Push event (may select others if needed)
    - for Multibranch Pipeline, install the 'Multibranch Scan Webhook Trigger' plugin in Jenkins
        - select one of the branches in the multibranch pipeline and go to 'Configure'
        - a new option 'Scan by Webhook' will show under the 'Scan Multibranch Pipeline Triggers' section
        - add a Trigger token (can be named to your liking. ex: githubtoken etc), when click on ? it will generate a url in which provide your token name, this will be used for communication between GitHub and Jenkins
        - then in github, do the same steps as above for adding a webhook
            - this time the Payload URL will be what is given in the section where you declare the Trigger token in Jenkins (may have to click the question mark)
- if using GitLab
    - install the Gitlab plugin in Jenkins
    - go to 'Manage Jenkins' > 'Configure System', should now see a newly added Gitlab section
    - make sure 'Enable Authentication for '/project' end-point' is checked
    - configure gitlab connections
        - enter connection name
        - enter the gitlab host url: https://gitlab.com/
        - add an api token
            - for 'Kind', choose 'Gitlab API token' (this is the Personal Access token configured in the settings from Gitlab)
    - in your pipeline job, there will now be a gitlab connection section (this is from the plugin)
    - configure build triggers in the 'Build Triggers' section
        - select the 'Build when a change is pushed to gitlab...' option
    - configure gitlab to send a notification to jenkins when a push or commit happens
        - in gitlab, got to 'Settings' > 'Integrations' > select 'Jenkins CI'
            - add the jenkins url (webhook url), enter jenkins username and password
    - for multibranch pipeline configuration, the setup will be the same as the above for github
---
---






