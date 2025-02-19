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
                    def serverProcess = sh(script: 'nohup node api/server.js &', returnStdout: true, start: true)
                    waitUntil {
                        try {
                            sh(script: 'curl -s http://localhost:3050', returnStatus: true) == 0
                        } catch (Exception e) {
                            return false
                        }
                    }
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
