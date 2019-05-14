pipeline {
    agent any

    tools {
        maven 'local-maven'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
