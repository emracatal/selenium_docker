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
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_HUB_USR', passwordVariable: 'DOCKER_HUB_PSW')]) {
                    bat "echo %DOCKER_HUB_PSW% | docker login -u %DOCKER_HUB_USR% --password-stdin"
                    bat "docker push emracdocker/selenium"
                }
            }  // Closing the 'steps' block for the "Push Image" stage
        }  // Closing the "Push Image" stage
    }  // Closing the 'stages' block
    post {
        always {
            bat "docker logout"
        }
    }
}
