pipeline {
    agent any

  environment {
      DH_USER = 'rahul3mukhe0405'
  }

  stage('Build Docker Image') {
      steps {
          bat """
              docker build -t ${DH_USER}/devops-flask-demo:${BUILD_NUMBER} ./app
              docker tag ${DH_USER}/devops-flask-demo:${BUILD_NUMBER} ${DH_USER}/devops-flask-demo:latest
          """
      }
  }

  stage('Push to Docker Hub') {
      steps {
          withCredentials([usernamePassword(credentialsId: 'docker-hub-creds',
                                          usernameVariable: 'DH_USER',
                                          passwordVariable: 'DH_PASS')]) {
              bat """
                  echo %DH_PASS% | docker login -u %DH_USER% --password-stdin
                  docker push %DH_USER%/devops-flask-demo:${BUILD_NUMBER}
                  docker push %DH_USER%/devops-flask-demo:latest
              """
          }
      }
  }
}