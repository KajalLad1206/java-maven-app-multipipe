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
            // when{
            //     expression{
            //         BRANCH_NAME == 'main'
            //     }
            // }
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
               buildImage() 
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