pipeline {
    agent { label 'worker' }

    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "test"
            }
        }

        stage("build") {
            steps {
                sh "docker build -t notes-app:test ."
            }
        }

        stage("deploy") {
            steps {
                sh "docker rm -f notes-app-test || true"
                sh "docker run -d -p 8002:8000 --name notes-app-test notes-app:test"
            }
        }
    }
}
