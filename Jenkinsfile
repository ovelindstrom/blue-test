pipeline {
    agent any
    options {
        timestamps()
        timeout(time: 1, unit: 'HOURS')
        buildDiscarder(logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '7', daysToKeepStr: '7', numToKeepStr: '7'))
        disableConcurrentBuilds()

    }
    tools {
        //jdk 'JDK8'
        maven 'M3'
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

        stage('Parallel Hello') {
            environment {
                DEPLOY_TO = "${params.DEPLOY_ENV}"
            }
            steps {
                parallel(
                        "Hello-Person": {
                            echo "Hello ${params.PERSON}!"
                            echo "Your current deploy environment is ${env.DEPLOY_TO}"
                            sh 'printenv'
                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'blue', imageUrl: '', messageLink: '', text: 'Hello-Person', thumbUrl: '', title: 'Hello-Person', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':wave:', message: "Hello ${params.PERSON}"
                        },
                        "Hello-Build": {
                            sh 'mvn -Dsettings.security=./settings-security.xml -s settings.xml -B clean deploy'
                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'yellow', imageUrl: '', messageLink: '', text: 'Building', thumbUrl: '', title: 'Building', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':baby:', message: 'Building'
                        },
                        "Hello-Sleep": {

                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'orange', imageUrl: '', messageLink: '', text: 'I am going to sleep', thumbUrl: '', title: 'Sleep', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':yawn:', message: 'Sleep'
                            sleep 5

                            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'orange', imageUrl: '', messageLink: '', text: 'I am awake', thumbUrl: '', title: 'Awake', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':yawn:', message: 'Awake!'
                        }
                )
            }
        }

        stage('Release') {
            when {
                branch 'master'
            }
            steps {
                script {

                    timeout(time: 60, unit: 'SECONDS') {

                        script {
                            def pom = readMavenPom file: 'pom.xml'

                            def releaseVersion = pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")

                            echo "Releasing version ${releaseVersion}"

                            sh "mvn -B -Dsettings.security=./settings-security.xml -s settings.xml -DreleaseVersion=${releaseVersion} -DdevelopmentVersion=${pom.version} -Dtag=v${releaseVersion} -DpushChanges=false -DlocalCheckout=true -DpreparationGoals=initialize release:prepare release:perform"
                        }

                    }
                }
            }
        }


        stage('Step version') {
            when {
                branch 'master'
            }
            steps {
                script {

                    timeout(time: 14, unit: 'MINUTES') {
                        rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'red', imageUrl: '', messageLink: '', text: "We need your input at ${env.RUN_DISPLAY_URL}", thumbUrl: '', title: 'Select release type', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':waiting:', message: "Input needed"

                        script {
                            def stepVersion = input id: 'StepVersion', message: 'Do you want to step the version?', parameters: [booleanParam(defaultValue: false, description: '', name: 'stepVersion')]
                            if (stepVersion) {
                                def developmentVersion = input id: 'NextVersion', message: 'What is the next version?'

                                sh "mvn -B -Dsettings.security=./settings-security.xml -s settings.xml -DdevelopmentVersion=${developmentVersion} release:update-versions"
                            }

                        }

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

    }

    post {
        always {
            echo "We are done!"
            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'green', imageUrl: '', messageLink: '', text: 'Bye', thumbUrl: '', title: 'Bye', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':checkered_flag:', message: 'My work is done!'
        }

        failure {
            echo "We are done, but something went wrong."
            rocketSend attachments: [[audioUrl: '', authorIcon: '', authorName: '', color: 'red', imageUrl: '', messageLink: '', text: 'ERROR', thumbUrl: '', title: 'ERROR', titleLink: '', titleLinkDownload: '', videoUrl: '']], channel: 'jenkins', emoji: ':error:', message: 'ERROR!'

        }
    }
}
}