pipeline {
    agent any
    parameters {
         string(name: 'tomcat_dev', defaultValue: '159.89.34.174', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '159.89.36.111', description: 'Production Server')
    }
    triggers {
         pollSCM('* * * * *')
     }
stages{
        stage('Build'){
            steps {
                sh '/Users/audreytan/documents/apache-maven-3.5.2/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp **/target/*.war audtan@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }
                stage ("Deploy to Production"){
                    steps {
                        sh "scp **/target/*.war audtan@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}

