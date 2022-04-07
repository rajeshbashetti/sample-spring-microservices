pipeline {
agent {
label 'buildserver'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo  docker login -uankit1111 -pmiet@1234 "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker tag account-service ankit1111/account-service "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker push ankit1111/account-service  "
        
        
    }
}
 
   
stage ('k8sdeployment') 
    {
       steps {
           node (' ansible') {
             sh " sudo ansible-playbook /etc/ansible/k8s.yaml"
   
    }
}
}
}
    
    
}
