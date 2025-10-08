pipeline {
    agent { label 'worker' }

    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Pulkit011Yadav/node-todo-cicd.git", branch: "master"
            }
        }

        stage("build") {
            steps {
                sh "docker build -t notes-app:latest ."
            }
        }

        stage("push to dockerhub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHUBCreds",
                    usernameVariable: "dockerHUBUser",
                    passwordVariable: "dockerHUBPass"
                )]) {
                    sh "echo $dockerHUBPass | docker login -u $dockerHUBUser --password-stdin"
                    sh "docker image tag notes-app:latest ${env.dockerHUBUser}/notes-app:latest"
                    sh "docker push ${env.dockerHUBUser}/notes-app:latest"
                }
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
