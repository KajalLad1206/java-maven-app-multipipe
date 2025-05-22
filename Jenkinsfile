#!/usr/bin/env groovy
def gv

pipeline{
    agent any

    stages{
        stage('test-app'){
            steps{
               echo "Testing the apllication...!"    
               echo "executing pipeline for $BRANCH_NAME"     
            }
        }
        stage('build'){
            // when{
            //     expression{
            //         BRANCH_NAME == 'main'
            //     }
            // }
            steps{
               echo "Building the apllication..!"  
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