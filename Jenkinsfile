pipeline {
    agent { label 'worker' }

    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "dev"
            }
        }

        stage("build") {
            steps {
                sh "docker build -t notes-app:dev ."
            }
        }

        stage("deploy") {
            steps {
                sh "docker rm -f notes-app-dev || true"
                sh "docker run -d -p 8001:8000 --name notes-app-dev notes-app:dev"
            }
        }
    }
}
