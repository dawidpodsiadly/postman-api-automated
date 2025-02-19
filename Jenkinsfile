pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dawidpodsiadly/postman-api-automated'
            }
        }

        stage('Run API Server') {
            steps {
                dir('api') {
                    sh 'npm install'
                    sh 'node server.js &'
                }
            }
        }

        stage('Run Postman API Tests') {
            steps {
                sh 'newman run postman-collection.json'
            }
        }
    }
}
