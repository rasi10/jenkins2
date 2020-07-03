
pipeline {
    agent none
    stages{     
        stage('Deploying application'){
            agent {
                docker { image 'node' }
            }
            steps {                
                sh '''
                    echo 'Application deployed successfully'
                '''                
            }
        }

        stage ('Front-end testing'){               
            agent {
                docker { image 'node' }
            }
            steps {
                sh '''
                    node -v
                    pwd
                    cd frontend-project/  
                    npm install && npm run test:report:regression   
                '''
            archiveArtifacts allowEmptyArchive: true, artifacts: 'frontend-project/cypress/videos/**'
            publishHTML([
                allowMissing: false, 
                alwaysLinkToLastBuild: false, 
                keepAll: false, 
                reportDir:'frontend-project/mochawesome-report', 
                reportFiles: 'mochawesome.html', 
                reportName: 'Front-end report', 
                reportTitles: ''])
            }      
                  
        }      
    }
}