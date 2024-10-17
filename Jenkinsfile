
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
    
    agent any
    
    stages {
        
        stage('Build and Test') {
            steps {
               
                    // Check the docker-compose version
                    //sh ‘docker-compose –version’
                    
                    // Bring up the services
                    //sh ‘docker-compose up -d’
                    
                    // Ensure the services are running
                    //sh ‘docker-compose ps’
                    
                    // Run tests on the correct service (adjust if necessary)
                    //sh ‘docker-compose exec -T wordpress /bin/bash -c “apt-get update && apt-get install -y maven && mvn test”‘

                    sh 'apt-get update && apt-get install -y sudo'
                    sh 'sudo su'
                
                    sh 'apt-get update'
                    sh 'apt-get install -y docker.io'
                    sh 'systemctl start docker'
                    sh 'systemctl enable docker'
                
                    sh 'docker build --tag "my-python-app"'
                
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
