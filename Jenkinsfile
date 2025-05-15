#!/usr/bin/env groovy

@Library('jenkins-shared-library')_
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
               buildJar() 
            }
        }
        stage('image-build'){           
            steps{
                script{
                    echo "Building image..!" 
                    buildImage('kajallad126/java-maven-app:1.5') 
                    dockerLogin()
                }
            }
        }
        stage('image-push'){           
            steps{
                script{
                    echo "Pushing image to dockerhub..!" 
                    dockerImagePush('kajallad126/java-maven-app:1.5') 
                }
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
            }
        }
    }
}