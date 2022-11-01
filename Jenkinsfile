pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.6'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds() // 禁止同時執行多次Pipeline
        retry ( 2 ) //總重試次數，放在 Stage下為 stage的重試次數
        // timeout(time: 10, unit: 'HOURS') // SECONDS/MINUTES/HOURS
    }
    stages {
       stage('stash') {
            agent { label "master" }
            steps {
                writeFile file : "a.txt", text : "$BUILD_NUMBER"
                stash(name "abc", include: "a.txt" )
            }
       }
       stage('unstash') {
            agent { label "node2" }
            steps {
                script {
                    unstash(name: "abc")
                    def content = readFile("a.txt")
                    echo "${content}"
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
