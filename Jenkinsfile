pipeline {
    agent any
    tools {
    maven 'localMaven'
  } 
  stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to staging'){
            steps{
                build job: 'Deploy-to-staging'
            }
        }
        stage('Deploy to prod'){
            steps{
                timeout(time:5, unit: 'DAYS'){
                    input message: 'Deploy to prod?'
                }

                build job: 'Deploy-to-prod'
            }
            post{
                success{
                    echo 'code deployed to prod.. Woo hoo'
                }
                failure{
                    echo 'SNAP.. Something broke'
                }
            }
        }
    }
}