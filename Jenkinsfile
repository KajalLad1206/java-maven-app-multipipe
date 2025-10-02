#!/usr/bin/env groovy
def gv

pipeline{
    agent any

    stages{
        stage('test'){
            steps{
               echo "Testing the apllication...!"    
               echo "executing pipeline for $BRANCH_NAME"     
            }
        }
        stage('build'){
            when{
                expression{
                    BRANCH_NAME == 'main'
                }
            }
            steps{
               echo "Building the application in multipipe...!"  
            }
        }
        
        stage('deploy'){
            when{
                expression{
                    BRANCH_NAME == 'main'
                }
            }
            steps{
                 echo "Deploying the apllication..!"  
            }
        }
    }
}