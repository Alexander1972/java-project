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
            post{
                success{
                    echo 'Now archiving ...'
                    archiveArtifacts artifacts: '**/target/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo 'Deploying....'
            }
        }
    }
}
