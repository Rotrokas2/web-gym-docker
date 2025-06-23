pipeline {
    agent any

    environment {
        BACKEND_IMAGE = 'web-gym-app-backend'
        FRONTEND_IMAGE = 'web-gym-app-frontend'
        CODECOV_TOKEN = credentials('CODECOV_TOKEN')  // Token como credencial segura
    }

    stages {
        stage('Verificar Docker') {
            steps {
                bat 'docker --version'
                bat 'docker ps'
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Juandarp96/web-gym-docker.git', branch: 'main'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('Backend') {
                    bat "docker build -t ${BACKEND_IMAGE} ."
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('Frontend') {
                    bat "docker build -t ${FRONTEND_IMAGE} ."
                }
            }
        }

        stage('Run Tests Backend') {
            steps {
                dir('Backend') {
                    bat """
                    docker run --rm ${BACKEND_IMAGE} npm test -- --coverage
                    """
                }
            }
        }

        stage('Upload Coverage to Codeco
