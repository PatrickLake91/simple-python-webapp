pipeline {
    agent any

    stages {
       stage('Clone') {
    steps {
        git branch: 'main', url: 'https://github.com/PatrickLake91/simple-python-webapp.git'
    }
}

        stage('Build Docker image') {
            steps {
                script {
                    dockerImage = docker.build("patricklake/simplewebapp:latest")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u patricklake --password-stdin'
                    sh 'docker push patricklake/simplewebapp:latest'
                }
            }
        }
    }
}
