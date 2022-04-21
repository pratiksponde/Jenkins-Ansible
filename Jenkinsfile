node
{
    stage('Continuous Download')
     {
    git 'https://github.com/pratiksponde/Docker-Jenkins.git'
    }
    stage('Continuous Build')
     {
    def mvnHome = tool name: 'maven-3', type: 'maven'
    def mvnCMD = "${mvnHome}/bin/mvn"
    sh "${mvnCMD} clean package"
  
    }
    stage('Build Docker Image')
     {
    sh 'docker build -t torretto/jenkins-jobs:v2 .'
    }
    stage('Push Docker Image')
     {
    withCredentials([string(credentialsId: 'password', variable: 'dockerHubPass')]) 
    {
    sh "docker login -u torretto -p ${dockerHubPass}"
    }    
    sh 'docker push torretto/jenkins-jobs:v2'
    }
    stage('Deploy Docker Container on Server')
     { 
    def dockerRun = 'sudo docker run -p 8080:8080 -d --name my-app torretto/jenkins-jobs:v2'
    sshagent(['Deployment-server']) 
    {
    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.93 ${dockerRun}"
     }
    }
}
