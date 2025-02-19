pipeline {
    agent any


    stages {
        stage('Run Postman Collection') {
            steps {
                git branch: 'main', url: 'https://github.com/dawidpodsiadly/postman-api-automated'
                sh 'newman run postman-collection.json'
            }
        }
    }
}
