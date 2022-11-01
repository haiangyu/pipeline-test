pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.6'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds() // 禁止同時執行多次Pipeline
        retry ( 4 ) //總重試次數，放在 Stage下為 stage的重試次數
        timeout(time: 10, unit: 'HOURS') // SECONDS/MINUTES/HOURS
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
        stage('Example') {
            steps {
                script {
                    def browsers = ['chrome', 'firefox']
                    for (int i = 0; i < browsers.size(); ++i) {
                        echo "Test the ${browsers[i]} browser"
                    }
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
