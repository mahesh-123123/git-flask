pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/mahesh-123123/git-flask.git'
            }
        }
       /* stage('Maven Build') {
            steps {
                bat 'mvn clean'
                bat 'mvn install'
                bat 'mvn package'
            }
        }*/
        stage('Build Docker Image') {
            steps {
                script {
                  //bat 'docker build -t maheshreddy123/nnn:v6 .'
                  //bat 'docker run -itd -p 9090:80 maheshreddy123/nnn:v6'  
                 sh 'docker build -t maheshreddy123/flask:v8 .'
                 sh 'docker run -itd -p 80:4000 maheshreddy123/flask:v8'  
                }
            }
        }
        
          
        
        stage('Push Docker Image in dockerhub') {
            steps {
                script {
                   /* withDockerRegistry(credentialsId: 'dockerhub',  url: '') {
                //bat 'docker push maheshreddy123/nnn:v6'
               bat 'docker push maheshreddy123/flask:v2'
               }*/
                    withCredentials([string(credentialsId: 'dockerhup', variable: 'dockerhp')]) {
                        sh "docker login -u maheshreddy123 -p ${dockerhp}"
                       
                    }
                            sh 'docker push maheshreddy123/flask:v8'     
              }
            }
          }
        stage('Run Container on server1 and sever2'){
            steps {
                sshagent(['server1']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.0.161 'docker run -p 80:4000 -d maheshreddy123/flask:v8'"
                }
                sshagent(['server1']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.45.251 'docker run -p 80:4000 -d maheshreddy123/flask:v8'"
                }
                
            }
                
        }
        
    }
}
