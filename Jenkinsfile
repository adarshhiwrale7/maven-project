pipeline {
    agent any
    parameters {
            string(defaultValue: 'test', description: 'default variable', name: 'var1')
        }

    triggers {
           pollSCM('* * * * *')
    }

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
                   sh 'echo "$var1"'
                }
                   
                
            }
        }
}