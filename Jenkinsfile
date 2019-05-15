pipeline {

    agent any

    tools {
        maven 'local-maven'
    }

    triggers {
        pollCSM(' * * * *')
    }

    parameters {
        string(name: 'paramName1', defaultValue: "defaultValue1", description: 'param 1 descr')
        string(name: 'paramName2', defaultValue: "defaultValue2", description: 'param 2 descr')
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
                echo "Testing.. ${parameters.paramName1} and ${parameters.paramName2}"
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
