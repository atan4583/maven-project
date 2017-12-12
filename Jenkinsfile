pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh '/Users/audreytan/documents/apache-maven-3.5.2/bin/mvn clean'
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
