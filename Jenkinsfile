pipeline {
  agent {
    docker {
      image 'maven:3.5.0-jdk-8-alpine'
    }
    
  }
  stages {
    stage('') {
      steps {
        parallel(
          "Hello1": {
            echo 'Hello1 World ${env.name}'
            
          },
          "Hello2": {
            echo 'Hello2 World ${env.name}'
            
          }
        )
      }
    }
  }
  environment {
    name = 'ove'
    sex = 'male'
    deploy = 'true'
  }
}