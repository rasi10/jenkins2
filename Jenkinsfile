
pipeline {
    agent none
    stages{     
        stage('Deploying application'){
            agent {
                docker { image 'cypress/base' }
            }
            steps {                
                sh '''
                    echo 'Application deployed successfully'
                '''                
            }
        }

        stage ('Front-end testing'){               
            agent {
                docker { image 'cypress/base' }
            }
            steps {
                sh '''
                    node -v
                    pwd
                    cd frontend-project/  
                    npm install 
                    npm run test:report:regression   
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