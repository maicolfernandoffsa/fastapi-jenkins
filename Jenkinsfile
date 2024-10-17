
import org.jenkinsci.plugins.docker.workflow.*
import org.jenkinsci.plugins.workflow.steps.*
    
/* Project settings */
def project="INCT"
/* Mail configuration*/
// If recipients is null the mail is sent to the person who start the job
// The mails should be separated by commas(',')
def recipients              = ""
def deploymentEnvironment   = "dev"
def inputtext = params.INPUT_TEXT

// Jira Server and Xray Server

private static final String DOCKER_PYTHON = "bcp/python39:2.0.0"
pipeline {
    
    agent {
      docker {
        image 'python:3'
        label 'my-build-agent'
      }
    }
    
    stages {
            stage('Instalar dependencias') {
                steps {
                    sh 'pip3 install -r requirements.txt'
                }
            }
            stage('Ejecutar pruebas') {
                steps {
                    sh 'python3 -m unittest discover'
                }
            }
            stage('Desplegar') {
                steps {
                    sh 'python3 main.py'
                }
            }
        
        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying…'
                // Add your deploy steps here
            }
        }
    }
    post {
        always {
            echo 'Post actions'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
