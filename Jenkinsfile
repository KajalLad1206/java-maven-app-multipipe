#!/usr/bin/env groovy

@Library('jenkins-shared-library')_

pipeline{
    agent any

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
               echo "Building the apllication..!" 
               buildJar() 
            }
        }
        stage('build-jar'){
            // when{
            //     expression{
            //         BRANCH_NAME == 'main'
            //     }
            // }
            steps{
               echo "Building the apllication..!" 
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