pipeline {
    agent { label 'worker' }

    stages {
        stage("Checkout") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "test"
            }
        }

        stage("Build Docker") {
            steps {
                sh "docker build -t notes-app:test ."
            }
        }

        stage("Deploy") {
            steps {
                sh "sed -i 's/8000:8000/8002:8000/' docker-compose.yaml"
                sh "docker compose down || true"
                sh "docker compose up -d --build"
            }
        }
    }
}
