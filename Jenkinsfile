pipeline {
    agent any
    tools{
        maven "maven"
    }

    environment {
        DOCKER_CREDENTIALS = credentials('raswanth')  // Docker Hub Credentials ID
    }

    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/RASWANTHSABARISH/guvi-docker-war'
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean"
                sh "mvn install"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t raswanthsabarish/guvi-docker-war .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-cred') {
                        sh 'docker push raswanthsabarish/guvi-docker-war'
                    }
                }
            }
        }
    }
}
