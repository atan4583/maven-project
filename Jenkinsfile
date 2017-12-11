pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package2'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
