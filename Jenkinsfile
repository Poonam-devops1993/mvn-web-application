pipeline{
    agent any
    tools{
        maven 'Maven_3.9.9'
    }
    environment
    {
       buildNumber = "${BUILD_NUMBER}"
    }
    stages{
        stage('Checkout code to jenkins from github'){
            steps()
            {
               git branch: 'DevOpsBranch', url: 'https://github.com/Poonam-devops1993/mvn-web-application.git' 
            }
        }
        stage('Build Artifact Using Maven'){
            steps()
            {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image'){
            steps()
            {
                sh 'docker build -t 000746846547.dkr.ecr.ap-south-1.amazonaws.com/login-application:${buildNumber} .'
            }
        }
    }
}