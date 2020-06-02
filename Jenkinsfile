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
		        sh 'docker run -d --name app app:test'
		        sh '/bin/nc -vz localhost 80'
                sh 'docker stop app'
            }
        }
        stage('Push Registry') {
            steps {
                echo 'Deploying....'
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'password', usernameVariable: 'user')]) {
                    sh 'docker login -u $user -p $password'
                    sh 'docker tag app:test albapc/app:stable'
                    sh 'docker push albapc/app:stable'
                }
            }
        }
    }
}