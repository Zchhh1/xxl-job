pipeline {
    agent any
    environment {
        git_url     = "git@https://github.com/Zchhh1/xxl-job.git"
        remote_ip   = "192.168.66.50"
        remote_dir  = "/var/lib/jenkins/workspace/xxl-job/"
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
        timestamps()
    }
    stages {
        stage('Build') {
            steps {
                // 清理工作区
                cleanWs()
 
                // 检出源码
                checkout scm
 
                // 安装Maven依赖
                sh 'mvn clean install'
            }
        }
        stage('delete') {
            steps {
                echo '清理工作目录'
                cleanWs()
            }
        }
    }
    post {
        always {
            // 总是执行的步骤
            cleanWs() // 清理工作区
        }
    }

    post {
        success {
            sh "echo 成功了"
        }
        failure {
            sh "echo 失败了"
        }
    }
}
