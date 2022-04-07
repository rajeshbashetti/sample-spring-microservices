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
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo  docker login -urajesh741 -prajESH123# "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker tag account-service rajesh741/account-service "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker push rajesh741/account-service  "
        
        
    }
}
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
