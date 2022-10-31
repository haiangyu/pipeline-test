pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.6'
    }
    stages {
        stage('Build') {
            echo "build stage"
            // steps {
            //     sh "mvn clean package spring-boot:repackage"
            //     sh "printenv"
            // }
        }
        post {
            always {
                echo "stage post always"
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
