pipeline {
    agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_HUB_CREDS')
  }
 
    stages{
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sailusha/jenkins-new:1.0 .'
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
                sh 'docker push sailusha/jenkins-new:1.0'
               }
           }

    }
}
