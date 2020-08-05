pipeline {
    agent any 
    stages {
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("sfordlacework/lacework-cli")
                    app.inside {
                        sh 'lacework --help'
                    }
                }
            }
        }
    }
}
