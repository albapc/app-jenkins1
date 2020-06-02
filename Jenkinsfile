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
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh 'docker login -u $dockerHubUser -p $dockerHubPassword'
                    sh 'docker tag app:test $dockerHubUser/app:stable'
                    sh 'docker push $dockerHubUser/app:stable'
                    sh 'docker rm -f app'
                }
            }
        }
    }
}