pipeline {
    agent any

    stages {
        stage('Run Newman Collection') {
            steps {
                script {
                    sh 'docker run --rm postman/newman --version'
                    sh '''
                        docker run --rm \
                            -v ${WORKSPACE}:/etc/newman \
                            -w /etc/newman \
                            postman/newman run postman_collection.json \
                            --color off \
                            --disable-unicode
                    '''
                }
            }
        }
    }
}
