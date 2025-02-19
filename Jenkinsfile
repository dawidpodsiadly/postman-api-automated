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

        stage('Install API Server') {
            steps {
                dir('api') {
                    sh 'npm install'
                }
            }
        }

        stage('Run API Server') {
            steps {
                dir('api') {
                    sh 'node server.js'
                }
            }
        }

        stage('Run Postman Collection') {
            steps {
                sh 'newman run postman-collection.json'
            }
        }
    }

    post {
        failure {
            echo 'Job failed. Stopping the pipeline.'
            currentBuild.result = 'FAILURE'
        }
    }
}
