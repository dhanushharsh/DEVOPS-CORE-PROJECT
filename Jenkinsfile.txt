pipeline {
    agent any

    environment {
        DOCKERHUB = "harsh672/devops-project"
        CREDS = credentials('dockerhub-cred')
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/dhanushharsh/DEVOPS-CORE-PROJECT.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKERHUB}:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh 'echo $CREDS_PSW | docker login -u $CREDS_USR --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push ${DOCKERHUB}:latest'
            }
        }
    }
}
