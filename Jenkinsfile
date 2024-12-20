pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
        def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@35.182.83.102'
    }
    stages {
        
        stage('Build') {
            steps {
                echo 'building app'
                sh "pwd"
                sh "ls"
                sh "zip -r webapp.zip ."
                sh "ls"
            }
        }
        
       stage('Deploy') {
            steps {
                echo 'Deploying app'
               
            }
        }
        stage('Clean-Up') {
            steps {
                echo 'Remove existing files'
                deleteDir()
            }
        }
    }
}