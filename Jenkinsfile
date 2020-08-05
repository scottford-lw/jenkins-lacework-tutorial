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
        stage('Push Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        stage('Lacework Vulnerability Scan') {
            agent {
                docker { image 'techallylw/lacework-cli:latest' }
            }
            when {
                branch 'master'
            }
            steps {
                echo 'Running Lacework vulnerability scan'
                // sh 'lacework vulnerability scan run index.docker.io selacework/sample-nodejs-app latest --poll --noninteractive'
                sh 'env'
            }
        }
    }
}
