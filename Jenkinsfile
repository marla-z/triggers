pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
        timestamps() 
    }
    environment {
        BRANCH = "${GIT_BRANCH.split('/').last()}"
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Get All Environment Variables') {
            steps {
                script {
                    println "${BRANCH}"
                }
            }
        }
    }
}