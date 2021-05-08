pipeline{
    agent any

tools {nodejs "nd"}
    
    stages{
        stage('Test'){
            steps{
                echo 'Testing app...'
                sh 'npm install'
                sh 'npm run test' 
            }     
        }    
    }
    post{
        always{
            junit 'reports/**/*.xml' 
            step([
                    $class              :"CloverPublisher",
                    cloverReportDir     :"build/coverage",
                    xloverReportFileName:"clover.xml"
            ])
        }
        failure{
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                to: 'olakrason1999@gmail.com',
                subject: "Jenkins build failed ${env.BUILD_NUMBER}"
            
        }
    } 

    
}
