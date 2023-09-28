pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
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
                    sh 'env'
                }
            }
        }
    }
    post {
        always {
            wrap([$class: 'TimestamperBuildWrapper']) {
                println "end"
            }
        }
    }
}

def SetEnv() {
    print "env"
}