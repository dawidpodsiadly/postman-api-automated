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

        stage('Run API Server and Test Postman') {
            steps {
                script {
                    sh 'node api/server.js &'
                    sleep 20
                    dir('/') {
                        sh 'newman run postman-collection.json'
                    }
                }
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
