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
                sh "docker compose down || true"
                sh "docker compose up -d --build"
            }
        }
    }
}
