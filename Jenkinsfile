pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
            CI = 'true'
            HOME = '.'
        }
    stages {
        stage('Build') {
            steps {
                    sh 'docker-compose -f docker-compose.yaml up -d --build'
            }   
        }
          stage('Build Back') {
            steps {
                dir("./server") {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
                    steps {
                        sh './jenkins/scripts/test.sh'
                    }
                }
                stage('Deliver') {
                            steps {
                                sh './jenkins/scripts/deliver.sh'
                                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                                sh './jenkins/scripts/kill.sh'
                            }
                        }

    }
}
