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
                bat "docker push emracdocker/selenium"
                echo %DOCKER_HUB_PSW% | docker login -u %DOCKER_HUB_USR% --password-stdin
            }
        }
    }
    post {
        always {
            bat "docker logout"
        }
    }
}
