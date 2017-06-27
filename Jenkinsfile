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
                timeout(time: 30, unit: 'SECONDS') {
                    script {

                        def wantChips = input id: 'mcd', message: 'Do you want chips whit that?', ok: 'Yes', submitterParameter: 'approver'
                        echo "Ok ${params.approver} you ${wantChips}!"
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
        stage("Parallels") {
            steps {
                parallel(
                        "master": {
                            stage("P-Master") {
                                when {
                                    branch 'master'
                                }
                                steps {
                                    echo "Parallels - P-Master"
                                }
                            }
                        },
                        "slave": {
                            stage("P-Slave") {
                                when {
                                    branch 'slave'
                                }
                                steps {
                                    echo "Parallels - P-Slave"
                                }
                            }
                        },
                        "both-but-not-feature": {
                            stage("P-Both") {
                                when {
                                    anyOf { branch 'slave'; branch 'master' }
                                }
                                steps {
                                    echo "Parallels - Both but never anything else"
                                }
                            }
                        },
                        "parameter": {
                            stage("P-parameter") {
                                when {
                                    environment name: 'DEPLOY_ENV', value 'dev'

                                }
                                steps {
                                    echo "Deploying to DEV"
                                }
                            }
                        }
                )
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
