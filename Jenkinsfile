pipeline {
    agent any
    stages{
        stage('build'){
            steps{
               mvn 'clean package'
            }
            post{
                success {
                    echo 'Now archiving artifacts..'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
    }
}