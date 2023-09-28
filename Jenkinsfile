pipeline {
    agent { label 'runner' }
    stages {
        wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'xterm']) {
            step([$class: 'WsCleanup'])
            wrap([$class: 'TimestamperBuildWrapper']) {
                stage("Env") {
                    SetEnv()
                }
            }
        }
    }
}
