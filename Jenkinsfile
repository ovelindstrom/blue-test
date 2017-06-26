pipeline {
    agent any
    environment {
        DEPLOY_TO = 'default'
    }
    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
        string(name: 'PERSON', defaultValue: 'mr Bean', description: 'Who\'s there?')
    }
    stages {
        stage('Init'){
            steps{
                echo "This is just a demo."
            }
        }

        stage('Say Hello') {
            environment {
                DEPLOY_TO = "${params.DEPLOY_ENV}"
            }
            steps {
                parallel(
                        "Hello1": {
                            echo "Hello ${params.PERSON}!"
                            sh 'printenv'
                        },
                        "Hello2": {
                            echo "Your current deploy environment is ${env.DEPLOY_TO}"
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
                echo "Ok {approver}!"
            }
        }
        stage('Slave') {
            when{
                not {branch 'master'}
            }
            steps {
                echo "YOU ARE NOT MY MUM!!!"

            }
        }
    }
}