// pipeline{
//     agent any
//     stages{
//            stage("Build Jar"){
//                 steps{
//                     bat "mvn clean package -DskipTests"
//                 }
//            }
//            stage("Build Image"){
//                  steps{
//                      bat "docker build -t=emracatal/selenium ."
//                  }
//            }
//            stage("Push Image"){
//                  environment{
//                        DOCKER_HUB = credentials('dockerhub-creds')
//                  }
//                  steps{
//                       bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
//                       bat "docker push emracatal/selenium"
//                  }
//            }
//     }
//
//     post{
//         always{
//             bat "docker logout"
//         }
//     }
// }
//
pipeline{
    agent any
    stages{
           stage("Build Jar"){
                steps{
                    bat "mvn clean package -DskipTests"
                }
           }
           stage("Build Image"){
                 steps{
                     bat "docker build -t=emracatal/selenium:latest ."
                 }
           }
           stage("Push Image"){
                 environment{
                       DOCKER_HUB = credentials('dockerhub-creds')
                 }
                 steps{
                      bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
                      bat "docker push emracatal/selenium:latest"
                      bat "docker tag emracatal/selenium:latest emracatal/selenium:%BUILD_NUMBER%"
                      bat "docker push emracatal/selenium:%BUILD_NUMBER%"

                 }
           }
    }

    post{
        always{
            bat "docker logout"
        }
    }
}
