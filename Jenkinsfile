/*
pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps {
                build job: 'Deploy-to-staging'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
            
            
            
        }


    }
}
*/

pipeline {
  agent any

  environment {
    // FOO will be available in entire pipeline
    FOO = "PIPELINE"
  }

  stages {
    stage("local") {
      environment {
        // BAR will only be available in this stage
        BAR = "STAGE"
      }
      steps {
        sh 'echo "FOO is $FOO and BAR is $BAR"'
      }
    }
    stage("global") {
      steps {
        sh 'echo "FOO is $FOO and BAR is $BAR"'
      }
    }
  }
}
