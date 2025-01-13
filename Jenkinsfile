pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
        def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@35.183.238.42'
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
        stage('artifact') {
            steps {
                echo 'pushing artifact to nexus'
                sh "curl -u admin:admin123 --upload-file webapp.zip http://15.223.0.27:8081/repository/webapp/webapp.zip"
                
            }
        }
       stage('Deploy') {
            steps {
                echo 'Deploying app'
                sshagent(['server-key']) {
                    sh '$CONNECT "curl -u admin:admin123 -O http://15.223.0.27:8081/repository/webapp/webapp.zip"'
                    sh '$CONNECT "sudo apt install zip -y"'
                    sh '$CONNECT "sudo rm -rf /var/www/html/"'
                    sh '$CONNECT "sudo mkdir /var/www/html/"'
                    sh '$CONNECT "sudo unzip webapp.zip -d /var/www/html/"'                    
                }
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