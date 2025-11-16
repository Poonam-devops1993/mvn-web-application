pipeline 
{
    agent any
    tools
    {
        maven  'Maven_3.9.7'
    }

     environment{
       buildNumber = "${BUILD_NUMBER}"
    }
    
        stages{
            stage('Git Checkout')
            {
                steps()
                {
                    git branch: 'DevOpsBranch', url: 'https://github.com/Poonam-devops1993/mvn-web-application.git'
                }
            }
          
            stage('Build Project')
            {
                 steps()
                {
                       sh 'mvn clean package'
                }
            }
            stage('Build Docker Image')
            {
                steps()
                {
                    sh 'docker build -t poonam2019/dockerpipeline:${buildNumber} .'
                }
            }
            stage('Push Docker Image to DockerHub Registry')
            {
                steps()
                {
                    withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')]) 
                    {
                       sh 'docker login -u poonam2019 -p ${Docker_Hub_Password}'
                    }
                       sh 'docker push poonam2019/dockerpipeline:${buildNumber}'
                }
            }
            stage('Delete Docker Image Locally In Jenkin Build Server')
            {
                steps()
                {
                        sh 'docker rmi -f poonam2019/dockerpipeline:${buildNumber}'
                }
            }
            stage('Deploy Application to Deployment server')
            {
                steps()
                {
                    sshagent(['DeploymentServer_SSH'])
                     {
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@13.233.124.110 docker rm -f mvnwebapplication || true"
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@13.233.124.110 docker run -d --name mvnwebapplication -p 8080:8080 poonam2019/dockerpipeline:${buildNumber}"
                           
                        
                     }     
                }
            }
        
        }
    }
