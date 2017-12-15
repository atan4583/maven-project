pipeline {
    agent any
    parameters {
         string(name: 'tomcat_server', defaultValue: 'localhost', description: 'Tomcat Server')
         string(name: 'tomcat1_folder', defaultValue: '/Users/audreytan/documents/JenkinsDemo/apache-tomcat-8.5.24-prod/webapps', description: 'Production Server')
        string(name: 'tomcat2_folder', defaultValue: '/Users/audreytan/documents/JenkinsDemo/apache-tomcat-8.5.24-staging/webapps', description: 'Staging Server')
    }
    triggers {
         pollSCM('* * * * *')
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
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "cp **/target/*.war jenkins@${params.tomcat_server}:${tomcat1_folder}"
                    }
                }
                stage ("Deploy to Production"){
                    steps {
                        sh "cp **/target/*.war jenkins@${params.tomcat_server}:${tomcat2_folder}"
                    }
                }
            }
        }
    }
}

