pipeline {
    agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    tools{
        maven 'mymaven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ramalaxmibandi/jenkins-docker']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t ramalaxmi/devops-integration:1.0 .'
                }
            }
        }
        stage('Login') {
            steps {
                 sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
       stage('Push image to Hub') {
           steps {
                sh 'docker push ramalaxmi/devops-integration:1.0'
               }
           }

    }
}
