pipeline {
    agent any
    tools {
        jdk 'java8'
        maven 'maven3'
    }
        stages{
            stage ("Init") {
                steps{
                   sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                   '''
                }
            }
            stage ("Build") {
                steps{
                   sh 'mvn clean package checkstyle:checkstyle'
                }
                   post{
                       success{
                           echo "Archiving Artifacts"
                           archiveArtifacts '**/*.war'
                           echo "Junit test"
                           junit '**/target/surefire-reports/*.xml'
                           echo "Code Quality"
                           checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''

                       }
                   }
                
            }
            stage ("Deploy"){
                steps{
                    build "deploytodev"
                }
            }
            stage ("Delivery"){
                steps{
                    timeout(2) {
                    //2minutes
                    }
                    input 'Do you want to deploy code to production?'

                    build 'deploytoprod'
                }
            }
    
        }
}