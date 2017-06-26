pipeline {
  agent any
  stages {
    stage('Hello hey!') {
      steps {
        parallel(
          "Hello1": {
            echo '"Hello1 World ${params.name}"'
            sh 'printenv'
            
          },
          "Hello2": {
            echo 'Hello2 World'
            
          }
        )
      }
    }
    stage('Master') {
      when {
        branch 'master'
      }
      steps {
        input(id: 'Mcd', message: 'Do you want chips whit that?', ok: 'Yes', submitterParameter: 'approver')
        echo 'Ok {approver}!'
      }
    }
    stage('Slave') {
      when {
        not {
          branch 'master'
        }
        
      }
      steps {
        echo 'YOU ARE NOT MY MUM!!!'
      }
    }
    stage('Depoy to Test') {
      steps {
        timestamps() {
          input 'Deploy to Test?'
        }
        
      }
    }
  }
  parameters {
    string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
    string(name: 'PERSON', defaultValue: 'mr Bean', description: 'Who\'s there?')
  }
}