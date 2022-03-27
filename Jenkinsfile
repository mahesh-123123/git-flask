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
                 sh 'docker build -t maheshreddy123/flask:v2 .'
                 sh 'docker run -itd -p 9999:4000 maheshreddy123/flask:v2'  
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
                        withCredentials([usernameColonPassword(credentialsId: 'dockerhub', variable: 'dockerhubp')]) {
                            sh "docker login -u maheshreddy123 -p ${dockerhubp}"
                        }
                            sh 'docker push maheshreddy123/flask:v2'     
              }
            }
          }
        
    }
}
