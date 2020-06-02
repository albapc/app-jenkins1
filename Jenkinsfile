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
		        sh 'docker run --rm --name app -id -p 80:80 app:test'
		        sh '/bin/nc -vz localhost 80'
            }
	        post {
		        always {
		            sh 'docker container stop app'
		        }
	        }
        }
        stage('Push Registry') {
            steps {
                echo 'Deploying....'
                sh 'docker tag app:test albapc/app:stable'
                sh 'docker push albapc/app:stable'
            }
        }
    }
}
