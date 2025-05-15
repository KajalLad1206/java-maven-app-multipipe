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
        stage('build-image'){
            // when{
            //     expression{
            //         BRANCH_NAME == 'main'
            //     }
            // }
            steps{
               echo "Building Image..!" 
               buildImage('kajallad126/java-maven-app:1.5') 
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