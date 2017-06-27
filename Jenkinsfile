pipeline {
    agent any
    options {
        timestamps()
        timeout(time:1, unit: 'HOURS')
        buildDiscarder(logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '7', daysToKeepStr: '7', numToKeepStr: '7'))
        disableConcurrentBuilds()

    }
    environment {
        DEPLOY_TO = 'default'
    }
    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
        string(name: 'PERSON', defaultValue: 'mr Bean', description: 'Who\'s there?')
    }
    stages {
        stage('Init') {
            steps {
                echo "This is just a demo."
                rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'green', imageUrl: '', messageLink: '', text: 'Starting', thumbUrl: '', title: 'Starting', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':clapper:', message: 'Hi from Jenkins'
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
                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'blue', imageUrl: '', messageLink: '', text: 'Hello', thumbUrl: '', title: 'Hello1', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':wave:', message: 'Hello1'
                        },
                        "Hello2": {
                            echo "Your current deploy environment is ${env.DEPLOY_TO}"
                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'yellow', imageUrl: '', messageLink: '', text: 'Hello', thumbUrl: '', title: 'Hello2', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':baby:', message: 'Hello2'
                        },
                        "Hello3": {
                            sleep 20

                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'orange', imageUrl: '', messageLink: '', text: 'I am awake', thumbUrl: '', title: 'Awake', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':yawn:', message: 'Hello2'
                        }
                )
            }
        }
        stage('Master') {
            when {
                branch 'master'
            }
            steps {
                script {

                    timeout(time: 30, unit: 'SECONDS') {
                        rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'red', imageUrl: '', messageLink: '', text: 'Input waiting', thumbUrl: '', title: 'Input waiting', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':waiting:', message: 'We need your input at ${env.RUN_DISPLAY_URL}'

                        script {
                            env.RELEASE_SCOPE = input id: 'release', message: 'What sort of release is it?', ok: 'Release!',
                                    parameters: [choice(name: 'RELEASE_SCOPE', choices: 'patch\nminor\nmajor', description: 'What is the release scope?')]
                        }
                        echo "${env.RELEASE_SCOPE}"
                    }
                }
            }
        }

        stage('Slave') {
            when {
                not { branch 'master' }
            }
            steps {
                echo "YOU ARE NOT MY MUM!!!"
                rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'blue', imageUrl: '', messageLink: '', text: 'Slave', thumbUrl: '', title: 'Slave', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':woman:', message: 'YOU ARE NOT MY MUM!!'

            }
        }


        stage('End') {
            steps {
                echo "We are done!"
                rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'green', imageUrl: '', messageLink: '', text: 'Bye', thumbUrl: '', title: 'Bye', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':checkered_flag:', message: 'My work is done!'
            }
        }
    }
}
