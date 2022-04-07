pipeline {
agent {
label 'build.javamachine'
}

stages {

stage ('Checkout1') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build1') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/16thnovdevopsjava/account-service ; mvn clean install " 
    }
}
    stage ('dockerbuild ') 
{
    steps
    {
      sh "cd /home/ubuntu/workspace/16thnovdevopsjava/account-service ; sudo docker build -t javaimage16th . " 
    }
}
    
    stage ('dockerimagepushing')
    {
        steps {
            sh "cd /home/ubuntu/workspace/16thnovdevopsjava/account-service ; sudo docker login -uankit1111 -pmiet@1234 "
            sh " cd /home/ubuntu/workspace/16thnovdevopsjava/account-service; sudo  docker tag javaimage16th  ankit1111/javamsaccountservic "
            sh " cd /home/ubuntu/workspace/16thnovdevopsjava/account-service; sudo docker push ankit1111/javamsaccountservic "
        }  
            
        }
    stage ('Deploying'){
        steps {
            node ('build.javamachine') {
                
                sh " cd /opt ; sudo ansible-playbook k8s.yaml"
                sh " cd /opt ; sudo ansible-playbook k8sservice.yaml"
            }
        }
    }   
}
    
}
