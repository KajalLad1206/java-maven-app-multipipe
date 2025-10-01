#!/usr/bin/env groovy

@Library('jenkins-shared-library')_ 

// If you want to load a shared library from Git without global config, you can define it inline using library() with a map of options.
// library identifier: 'my-shared-library@main',
//                             retriever: modernSCM([
//                                 $class: 'GitSCMSource',
//                                 remote: 'https://github.com/KajalLad1206/jenkins-shared-library.git',
//                                 credentialsId: 'github-credential'                                
//                             ])
pipeline{
    agent any
    tools{
        maven 'maven-3.9'
    }
    
    environment{
        IMAGE_NAME = 'kajallad126/java-maven-app:1.5'
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
                echo "Building image..!" 
                script{                    
                    dockerImageBuild(env.IMAGE_NAME) 
                    dockerLogin()
                }
            }
        }
        stage('image-push'){           
            steps{
                echo "Pushing image to dockerhub..!" 
                script{                    
                    dockerImagePush(env.IMAGE_NAME) 
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
                script{ 
                    sshagent(['app-deploy-server-key']) {
                        def dockercommand = "docker run -p 8080:8080 -d ${env.IMAGE_NAME}"
                        sh "ssh -o StrictHostKeyChecking=no kajal@34.130.221.92 ${dockercommand}"
                        }
                } 
            }
        }
    }
}