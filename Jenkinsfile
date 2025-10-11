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
                sh "docker build -t notes-app:tes ."
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
