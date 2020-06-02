pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            echo 'Building..'
          }
        }

        stage('Inicio') {
          steps {
            echo 'Hola desde stage inicio'
          }
        }

      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing..'
          }
        }

        stage('Test2') {
          steps {
            echo 'Hola desde stage2'
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying....'
      }
    }

  }
}