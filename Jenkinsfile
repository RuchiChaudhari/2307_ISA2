pipeline {
    agent any
    environment {
        // Explicitly setting the Docker path
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
        stage('List Files') {
            steps {
                dir('2307_ISA2') {
                    sh 'ls -l'
                }
            }
        }
        stage('Build') {
            steps {
                dir('2307_ISA2') {
                    sh 'docker build -t ruchi563/2307 -f Dockerfile .'
                }
            }
        }
        stage('Login') {
            steps {
                // Use Docker path to ensure login happens correctly
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin docker.io'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ruchi563/2307'
            }
        }

        stage('Delete') {
            steps {
                sh 'docker rm -f 2307 || true'
            }
        }        
        stage('Run in Daemon Mode') {
            steps {
                    dir('2307_ISA2') {
                    sh 'docker build -t ruchi563/2307 -f Dockerfile .'
                    sh 'docker run -d --name 2307 ruchi563/2307'
            }
        }
    }
}
