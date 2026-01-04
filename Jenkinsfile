pipeline{
    agent any
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
    }
}