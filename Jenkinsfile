pipeline {

    agent any

    tools {
        maven 'local-maven'
    }

    triggers {
        pollSCM('* * * * *')
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
                echo "Testing.. ${params.paramName1} and ${params.paramName2}"
            }
        }
        stage('Build image') {
            steps {
                echo 'Building image'
            }
            //app = docker.build("[id-of-your-project-as-in-google-url]/[name-of-the-artifact]")
        }
        stage('Push image') {
            steps {
                echo 'Pushing image'
            }
//            docker.withRegistry('https://eu.gcr.io', 'gcr:[credentials-id]') {
//                app.push("${env.BUILD_NUMBER}")
//                app.push("latest")
//            }

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
