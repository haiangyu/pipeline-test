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
    // 自定環境變數
    environment {
        CC = 'clang'
    }
    stages {
        stage('pmd') {
            steps {
                sh "mvn pmd:pmd"
            }
        }
        // stage("Example")
        // {
        //     environment{
        //         DEBUG_FLAGS = '-g'
        //     }
        //     steps{
        //         sh "${CC} ${DEBUG_FLAGS}"
        //         sh 'printenv'
        //         echo "${env.gname}"
        //         echo "Running ${env.BUILD_NUMBER} on ${env.JENKINS_URL}"
        //         echo "Running $env.BUILD_NUMBER on $env.JENKINS_URL"
        //         echo "Running ${BUILD_NUMBER} on ${JENKINS_URL}"
        //     }
        // }
    }
    post {
        changed {
            echo "pipeline post changed"
        }
        always {
            echo "pipeline post always"
            cleanWs()
            pmd(canRunOnFailed: true, pattern: '**/target/pmd.xml')
        }
        success {
            echo "pipeline post success"
        }
    }
}
