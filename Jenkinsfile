pipeline {
    agent any
    environment {
        DJANGO_SETTINGS_MODULE = 'todo.settings'
        DOCKER_IMAGE = 'todo'
        REGISTRY_CREDENTIALS = credentials('926c72b4-0578-41b0-9f9b-ad22c11ab622')
        registry = "sanjaybhavikatti/to-do-app"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build registry + ":${env.BUILD_ID}"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '926c72b4-0578-41b0-9f9b-ad22c11ab622') {
                        docker.image(registry + ":${env.BUILD_ID}").push('latest')
                    }
                }
            }
        }
    }
}
