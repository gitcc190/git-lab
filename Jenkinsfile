
peline {
    agent any
    
    environment {
        // 给镜像起个名字
        IMAGE_NAME = "my-jenkins-app"
    }

    stages {
        stage('拉取代码') {
            steps {
                echo '正在拉取代码...'
                // 注意这里写你的GitHub仓库地址
                git branch: 'main', credentialsId: 'github-ssh', url: 'git@github.com:你的用户名/git-lab.git'
            }
        }
        
        stage('构建镜像') {
            steps {
                echo '正在构建 Docker 镜像...'
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }
        
        stage('部署运行') {
            steps {
                echo '正在启动容器...'
                // 先停掉旧的，再起新的（|| true 是为了防止旧容器不存在时报错）
                sh 'docker stop $IMAGE_NAME || true'
                sh 'docker rm $IMAGE_NAME || true'
                sh 'docker run -d --name $IMAGE_NAME $IMAGE_NAME:latest'
            }
        }
    }
}pipeline {
