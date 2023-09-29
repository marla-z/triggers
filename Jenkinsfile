pipeline {
    agent { label "runner" }
 
    stages {
        stage('Перевірка Jenkinsfile') {
            steps {
                script {
                    if (fileExists('Jenkinsfile')) {
                        echo 'Файл Jenkinsfile був оновлений'
                    } else {
                        echo 'Файл Jenkinsfile залишився незмінним'
                    }
                }
            }
        }

        // Додай інші етапи тут
    }
}
