pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.6'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds() // 禁止同時執行多次Pipeline
    }
    stages {
        stage('Build') {
         
            steps {
                   echo "build stage"
            //     sh "mvn clean package spring-boot:repackage"
            //     sh "printenv"
            }
            post {
                always {
                    echo "stage post always"
                }
            }
        }
    }
    post {
        changed {
            echo "pipeline post changed"
        }
        always {
            echo "pipeline post always"
        }
        success {
            echo "pipeline post success"
        }
    }
}
