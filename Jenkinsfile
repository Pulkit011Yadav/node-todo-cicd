pipeline {
    agent { label 'worker' }
    environment {
        IMAGE_NAME = "nodesapp"
        TAG = "latest"
    }
    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "master"
            }
        }
        stage("build") {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${TAG} ."
            }
        }
        stage("push to dockerhub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerhub_creds",
                    usernameVariable: "U",
                    passwordVariable: "P"
                )]) {
                    sh "echo \"$P\" | docker login -u \"$U\" --password-stdin"
                    sh "docker image tag ${IMAGE_NAME}:${TAG} $U/${IMAGE_NAME}:${TAG}"
                    sh "docker push $U/${IMAGE_NAME}:${TAG}"
                    sh "docker logout"
                }
            }
        }
        stage("deploy") {
            steps {
                sh "docker compose down || true"
                sh "docker compose up -d --force-recreate"
            }
        }
    }
}
