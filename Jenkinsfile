#!/usr/bin/env groovy
def gv

pipeline{
    agent any

    stages{
        stage('test'){
            steps{
               echo "Testing the apllication...!"         
            }
        }
        stage('build'){
            steps{
               echo "Building the apllication..!"  
            }
        }
        
        stage('deploy'){
            steps{
                 echo "Deploying the apllication..!"  
            }
        }
    }
}