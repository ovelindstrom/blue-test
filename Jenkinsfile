pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        parallel(
          "Hello1": {
            echo 'Hello1 World!'
            sh 'printenv'
            
          },
          "Hello2": {
            echo 'Hello2 World'
            
          }
        )
      }
    }
  }
  environment {
    name = 'ove'
    sex = 'male'
    deploy = 'true'
    DOCKER_HOSTS = '192.168.99.100'
  }
}