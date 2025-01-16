pipeline {
    agent any
    stages {
        stage("Build Jar") {
            steps {
                bat "mvn clean package -DskipTests"
            }
        }
        stage("Build Image") {
            steps {
                bat "docker build -t=emracdocker/selenium ."
            }
        }
        stage("Push Image") {
            environment {
                DOCKER_HUB_CREDS = credentials('dockerhub-creds') // store credentials as a variable
            }
            steps {
                // Correct login command using the default environment variables
                bat "echo ${DOCKER_HUB_CREDS_USR} | docker login -u ${DOCKER_HUB_CREDS_USR} --password-stdin"
                bat "docker push emracdocker/selenium"
            }
        }
    }
    post {
        always {
            bat "docker logout"
        }
    }
}
