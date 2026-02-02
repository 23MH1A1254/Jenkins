pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23MH1A1254/Jenkins.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop adi-cont || true
                docker adi-cont || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi img-kokila || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t img-kokila .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 8082:8080 --name adi-cont img-kokila'
            }
        }
    }
}
