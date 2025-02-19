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
                script {
                    sh 'node api/server.js &'
                    sleep 10
                }
            }
        }

        stage('Run Postman Tests') {
            steps {
                sh 'newman run postman-collection.json'
            }
        }

        // stage('Stop API Server') {
        //     steps {
        //         script {
        //             sh 'pkill -f "node server.js"'
        //         }
        //     }
        // }
    }
}
