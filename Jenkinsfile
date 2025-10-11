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
                sh "docker compose down || true"
                sh "docker compose up -d --build"
            }
        }
    }
}
