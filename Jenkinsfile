pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
        timestamps() 
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
                    Env()
                }
            }
        }
    }
}

def Env() {
    sh "env"
}