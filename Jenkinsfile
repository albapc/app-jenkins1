pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
		        sh 'docker build -t app .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		        sh 'docker run -it app'
		        sh '/bin/nc -vz localhost 80'
                sh 'docker stop app'
            }
        }
        stage('Push Registry') {
            steps {
                echo 'Deploying....'
                sh 'docker tag app albapc/app:stable'
                sh 'docker push albapc/app:stable'
            }
        }
    }
}
