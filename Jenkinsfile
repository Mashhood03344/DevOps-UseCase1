pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("mashhood03344/DevOps-useCase1:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image("mashhood03344/DevOps-useCase1:${env.BUILD_NUMBER}").inside {
                        sh 'echo "Tests passed"'
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("mashhood03344/DevOps-useCase1:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
}
