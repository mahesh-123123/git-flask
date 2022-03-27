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
                 sh 'docker build -t maheshreddy123/flask:v3 .'
                 sh 'docker run -itd -p 5077:4000 maheshreddy123/flask:v3'  
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
                            sh 'docker push maheshreddy123/flask:v3'     
              }
            }
          }
        stage('Run Container on EC2-INSTANCE'){
            steps {
                sshagent(['EC2-INSTANCE']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@3.110.90.114 'docker run -p 4000:4000 -d maheshreddy123/falsk:v3'"
                }
                
               /* sshagent(['EC2-INSTANCE']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@13.232.65.99 'docker run -p 4000:4000 -d maheshreddy123/flask:v3'"
                  }*/
            }
        }
        
    }
}
