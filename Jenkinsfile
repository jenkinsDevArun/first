pipeline {
    agent any
    tools {
    maven 'localMaven'
    jdk 'localJDK'
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
        
    }
}
