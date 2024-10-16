pipeline {
    agent any
    tools {
        maven 'maven3.9.8' // 确保这里的名称与全局工具配置中的名称一致
    }
    environment {
        git_url     = "https://github.com/Zchhh1/xxl-job.git" // 修改为正确的 HTTPS URL
        remote_ip   = "192.168.66.50"
        remote_dir  = "/var/lib/jenkins/workspace/xxl-joba/"
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 20, unit: 'MINUTES')
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
                sh 'mvn -U clean package -Dmaven.test.skip=true '
                
                // 输出工作目录内容
                sh 'ls -la'
                
                // 归档构建产物
                archiveArtifacts artifacts: 'xxl-job-admin/target/*.jar', fingerprint: true
            }
        }
    }
}
