pipeline {
    agent any
    environment {
        PATH = "/usr/bin:/usr/local/bin:${env.PATH}" 
        DOCKER_USERNAME = 'ruchi563' // Your Docker username
        DOCKER_PASSWORD = 'abhiruchi1996' // Your Docker password
    }
    stages {
        stage('Clean and Clone Repository') {
            steps {
                cleanWs()
                sh 'git clone https://github.com/RuchiChaudhari/2307_ISA2.git'
            }
        }
        stage('Build') {
            steps {
                dir('2307_ISA2') {
                    sh 'docker build -t ruchi563/2307 -f Dockerfile .'
                }
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ruchi563/2307'
            }
        }
        stage('Delete') {
            steps {
                 sh 'docker rm -f 2307'
            }
        }
        stage('Run in Daemon Mode') {
            steps { 
                sh 'docker run -d --name 2307 ruchi563/2307'
            }
        }
    }
}
