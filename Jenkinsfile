#!/usr/bin/env groovy

//@Library('jenkins-shared-library')_
pipeline{
    agent any
    tools{
        maven 'maven-3.9'
    }

    stages{
        stage('test'){
            steps{
               echo "Testing the apllication...!"  
            }
        }
        stage('build-jar'){
           
            steps{
               echo "Building the jar..!" 
              // buildJar() 
            }
        }
        stage('image-build'){           
            steps{
                echo "Building image..!" 
                // script{                    
                //     dockerImageBuild('kajallad126/java-maven-app:1.5') 
                //     dockerLogin()
                // }
            }
        }
        stage('image-push'){           
            steps{
                echo "Pushing image to dockerhub..!" 
                // script{                    
                //     dockerImagePush('kajallad126/java-maven-app:1.5') 
                // }
            }
        }
        
        stage('deploy'){
            // when{
            //     expression{
            //         BRANCH_NAME == 'main'
            //     }
            // }
            steps{
                 echo "Deploying the apllication..!" 
                script{ 
                    sshagent(['app-deploy-server-key']) {
                        def dockercommand = 'docker run -p 8080:8080 -d kajallad126/java-maven-app:1.5'
                        sh "ssh -o StrictHostKeyChecking=no kajal@34.130.221.92 ${dockercommand}"
                        }
                } 
            }
        }
    }
}