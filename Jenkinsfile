pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
		        sh 'sudo docker build -t app:test .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		        sh 'sudo docker run -d --name app app:test'
		        sh '/bin/nc -vz localhost 80'
                sh 'sudo docker stop app'
            }
        }
        stage('Push Registry') {
            steps {
                echo 'Deploying....'
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'password', usernameVariable: 'user')]) {
                    sh 'sudo docker login -u $user -p $password'
                    sh 'sudo docker tag app:test albapc/app:stable'
                    sh 'sudo docker push albapc/app:stable'
                }
            }
        }
    }
}