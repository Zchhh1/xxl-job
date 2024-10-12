pipeline {
    agent any
    environment {
        git_url     = "https://github.com/Zchhh1/xxl-job.git" // 修正了 git_url 的格式
        remote_ip   = "192.168.66.50"
        remote_dir  = "/var/lib/jenkins/workspace/xxl-joba/"
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
 
                // 检出源码
                checkout scm
 
                // 安装Maven依赖
                script {
                    try {
                        sh 'mvn -U clean package -Dmaven.test.skip=true'
                    } catch (Exception e) {
                        error "Maven build failed: ${e.message}" // 错误处理
                    }
                }
            }
        }
    }
    post {
        always {
            // 总是执行的步骤
            cleanWs() // 清理工作区
        }
        success {
            echo '这不这么简单吗!' // 成功时的消息
        }
        failure {
            echo '失败咯.' // 失败时的消息
        }
    }
}
