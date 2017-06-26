pipeline {
    agent any
    environment
    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
        string(name: 'PERSON', defaultValue: 'mr Bean', description: 'Who\'s there?')
    }
    stages {
        stage('Startup'){
            echo "Hello ${params.PERSON}!"

        }
        stage('Hello hey!') {
            steps {
                parallel(
                        "Hello1": {
                            sh 'printenv'

                        },
                        "Hello2": {
                            echo 'Hello2 World'
                        }
                )
            }
        }
        stage('Master') {
            when{
                branch 'master'
            }
            steps {
                input id: 'Mcd', message: 'Do you want chips whit that?', ok: 'Yes', submitterParameter: 'approver'
                echo "Ok ${approver}!"
            }
            steps {
                environment name: 'DEPLOY_ENV', value: 'production'
                echo "Deploying to ${env.DEPLOY_ENV}"
            }
        }
        stage('Slave') {
            when{
                not {branch 'master'}
            }
            steps {
                echo "YOU ARE NOT MY MUM!!!"
                echo "Deploying to ${env.DEPLOY_ENV}"
            }
        }

        stage('Good bye!'){
            steps{
                echo 'CU!'
            }
        }

    }
}