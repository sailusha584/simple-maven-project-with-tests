pipeline {
    agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_HUB_CREDS')
  }
 
    stages{
        stage('Git'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sailusha584/simple-maven-project-with-tests']]])
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'sudo docker build -t sailusha/jenkins-repo:1.0 .'
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
                sh 'sudo docker push sailusha/jenkins-repo:1.0'
               }
           }

    }
}
