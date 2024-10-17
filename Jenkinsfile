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
