pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [[$class: 'CleanBeforeCheckout']], 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://github.com/Mashhood03344/DevOps-useCase1.git']]])
            }
        }
        stage('Build image') {
            steps {
                script {
                    def app = docker.build("mashhood03344/devops-usecase1")
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    // Run your tests here
                    echo 'Tests passed'
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
