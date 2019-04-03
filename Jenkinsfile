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
pipeline {
  environment {
    // environment variables and credential retrieval can be interspersed
    SOME_VAR = "SOME VALUE"
    // this assumes that "cred1" has been created on Jenkins Credentials
    CRED1 = credentials("cred1")
    INBETWEEN = "Something in between"
    // this assumes that "cred2" has been created in Jenkins Credentials
    CRED2 = credentials("cred2")
    // Env variables can refer to other variables as well
    OTHER_VAR = "${SOME_VAR}"
  }

  agent any

  stages {
    stage("foo") {
      steps {
        // environment variables are not masked
        sh 'echo "SOME_VAR is $SOME_VAR"'
        sh 'echo "INBETWEEN is $INBETWEEN"'
        sh 'echo "OTHER_VAR is $OTHER_VAR"'

        // credential variables will be masked in console log but not in archived file
        sh 'echo $CRED1 > cred1.txt'
        sh 'echo $CRED2 > cred2.txt'
        archive "**/*.txt"
      }
    }
  }
}
*/

pipeline {
    environment {
      /*
       * Uses a Jenkins credential called "FOOCredentials" and creates environment variables:
       * "$FOO" will contain string "USR:PSW"
       * "$FOO_USR" will contain string for Username
       * "$FOO_PSW" will contain string for Password
       */
      FOO = credentials("FOOcredentials")
    }

    agent any

    stages {
        stage("foo") {
            steps {
                // all credential values are available for use but will be masked in console log
                sh 'echo "FOO is $FOO"'
                sh 'echo "FOO_USR is $FOO_USR"'
                sh 'echo "FOO_PSW is $FOO_PSW"'

                //Write to file
                dir("combined") {
                    sh 'echo $FOO > foo.txt'
                }
                sh 'echo $FOO_PSW > foo_psw.txt'
                sh 'echo $FOO_USR > foo_usr.txt'
                archive "**/*.txt"
            }
        }
    }
}
