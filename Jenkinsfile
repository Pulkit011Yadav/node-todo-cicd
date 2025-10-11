pipeline {
    agent { label 'worker' }

    stages {
        stage("Checkout Code") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "test"
            }
        }

        stage("Build Docker Image") {
            steps {
                sh "docker build -t notes-app:test ."
            }
        }

        stage("Deploy Container") {
            steps {
                // Agar purana container hai toh remove kar do
                sh "docker rm -f notes-app-test || true"

                // Run the container with unique port and name
                sh "docker run -d -p 8002:8000 --name notes-app-test notes-app:test"
            }
        }
    }
}
