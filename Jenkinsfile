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

                        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_HUB_USR', passwordVariable: 'DOCKER_HUB_PSW')]) {
                                            // Using 'docker login' without echo for secure password input
                                            bat "docker login -u ${DOCKER_HUB_USR} --password-stdin <<< ${DOCKER_HUB_PSW}"
                                            bat "docker push emracdocker/selenium"
        }
    }
    post {
        always {
                    bat "docker logout"
                }
    }
}
