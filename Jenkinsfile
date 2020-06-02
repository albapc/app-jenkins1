pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'docker build -t app:test .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		sh '/bin/nc -vz localhost 22'
		sh '/bin/nc -vz localhost 80'
            }
        }
        stage('Push Registry') {
            steps {
                echo 'Deploying....'
		sh 'docker tag app:test app:stable'
		sh 'docker push app:test app:stable'
            }
        }
    }
}
