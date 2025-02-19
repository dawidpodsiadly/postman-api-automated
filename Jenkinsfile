pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/dawidpodsiadly/postman-api-automated'
            }
        }

        stage('Run API Server') {
            steps {
                dir('api-server') {
                    sh 'npm install'
                    sh 'node server.js &'
                }
            }
        }

        stage('Run Postman API Tests') {
            steps {
                dir('postman-api-tests') {
                sh 'newman run postman-collection.json'
                }
            }
        }
    }
}
