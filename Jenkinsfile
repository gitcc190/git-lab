pipeline {
    agent any
    
    environment {
        IMAGE_NAME = "my-jenkins-app"
    }

    stages {
        stage('拉取代码') {
            steps {
                echo '正在拉取代码...'
                git branch: 'main', credentialsId: 'github-ssh', url: 'git@github.com:gitcc190/git-lab.git'
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
                sh 'docker stop $IMAGE_NAME || true'
                sh 'docker rm $IMAGE_NAME || true'
                sh 'docker run -d --name $IMAGE_NAME $IMAGE_NAME:latest'
            }
        }
    }
}
