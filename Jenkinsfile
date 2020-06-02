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
		sh '/bin/nc -vz localhost 8080'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
