def approvalMap


pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.6'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds() // 禁止同時執行多次Pipeline
        retry ( 2 ) //總重試次數，放在 Stage下為 stage的重試次數
        timeout(time: 10, unit: 'HOURS') // SECONDS/MINUTES/HOURS
    }
    parameters {
        choice(name: 'CHOICES', choices: 'dev\ntest\nstaging', description: '請選擇部署的環境！')
    }
    // 自定環境變數
    environment {
        CC = 'clang'
    }
    stages {
        stage("test") {
            steps {
                approvalMap = input (
                    message : "發佈或停止",
                    ok : '確定',
                    parameters : [
                        choice(name: 'ENV', choices: 'dev\ntest\nstaging', description: '請選擇部署的環境！')
                        string(defaltValue: '', description: '', name: 'myparam')
                    ],
                    submitter : 'admin, admin2, releaseGroup',
                    submitterParamer: 'APPROVER'
                )
            }
        }
        stage("deploy"){
            steps {
                echo "操作者是： ${approvalMap['APPROVER']}"
                echo "發佈到什麼環境： ${approvalMap['ENV']}"
                echo "操作者是 ${approvalMap['myparam']}"
            }
        }
        // stage("deploy to test")
        // {
        //     when {
        //         expression { return params.CHOICES == 'test' }
        //     }
        //     steps {
        //         echo "deploy to test"
        //     }
        // }
        // stage("deploy staging")
        // {
        //     when {
        //         expression { return params.CHOICES == 'staging' }
        //     }
        //     steps {
        //         echo "deploy to staging"
        //     }
        // }
        
    }
}
