pipeline{
    agent any

    options {
      buildDiscarder logRotator(artifactDaysToKeepStr: '1', artifactNumToKeepStr: '2', daysToKeepStr: '1', numToKeepStr: '2')
      timestamps()
     }

    // agent{
    //     label "javaAgent"
    //      }
    //
    // tools{
    //      maven 'maven:3.6.3'
    //       }
    environment {
              DEPLOY = "${env.BRANCH_NAME == "python-dramed" || env.BRANCH_NAME == "master" ? "true" : "false"}"
              NAME = "${env.BRANCH_NAME == "python-dramed" ? "example" : "example-staging"}"
              def mvnHome =  tool name: "demo-maven:3.8.6", type: "maven"
              //def mavenCMD = "${mavenHome}/usr/share/maven"
              VERSION = "${env.BUILD_ID}"
              BUILD_NUMBER = "${env.BUILD_NUMBER}"
              BRANCH_NAME = "${env.BRANCH_NAME}"
              NODE_NAME = "${env.NODE_NAME}"
              REGISTRY = 'eagunuworld/mongodb-springboot-app'
              REGISTRY_CREDENTIAL = 'eagunuworld_dockerhub_creds'
            }

    stages {


      // stage('Example') {
      //      if (env.BRANCH_NAME == 'python-dramed') {
      //            echo 'I only execute on this environment $env.BRANCH_NAME'
      //          } else {
      //               echo 'I execute elsewhere'
      //              }
      //           }
      stage('checking... maven version ') {
          steps {
                  sh "mvn --version"
                   }
                }

      // stage(" Maven buld Artifacts Package"){
      //             def mavenCMD = "${mavenHome}/bin/mvn"
      //             sh "${mavenCMD} clean package"
      //           }

     stage('Build maven packages '){
              steps{
                    sh "mvn clean package"
                      }
                  }

 //      stage('Building Docker Images') {
 //                steps {
 //                  sh "sudo chmod 666 /var/run/docker.sock"
 //                  sh "docker build -t ${REGISTRY}:${VERSION} ."
 //                     }
 //                 }
 //
 //    stage('Push Docker Image To DockerHub') {
 //              steps {
 //                   withCredentials([string(credentialsId: 'eagunuworld_dockerhub_creds', variable: 'eagunuworld_dockerhub_creds')])  {
 //                   sh "docker login -u eagunuworld -p ${eagunuworld_dockerhub_creds} "
 //                   }
 //                 sh 'docker push ${REGISTRY}:${VERSION}'
 //                }
 //             }
 //    stage('Display All Files In Console') {
 //            steps {
 //               sh 'ls -lart'
 //            }
 //          }
 //
 //  stage('Update docker-compose Tag'){
 //      steps{
 //          	script{
 //          				    sh '''final_tag=$(echo $VERSION | tr -d ' ')
 //          				     echo ${final_tag}test
 //          				     sed -i "s/BUILD_TAG/$final_tag/g"  docker-compose.yml
 //          				     '''
 //          				  }
 //          			 }
 //          		}
 //  stage('Display docker-compose content ') {
 //        steps {
 //            sh 'cat docker-compose.yml'
 //            }
 //        }
 //
 //  stage('Stop And Remove Running Container') {
 //      steps{
 //          sshagent(['ec2-user-password-credentials']) {
 //               sh 'docker ps -f name=springboot -q | xargs --no-run-if-empty docker container stop'
 //               sh 'docker container ls -a -fname=springboot  -q | xargs -r docker container rm'
 //               sh 'docker container ls '
 //                  }
 //                }
 //             }
 //
 //  stage('Remove All Images Before Deployment') {
 //        steps{
 //            sshagent(['ec2-user-password-credentials']) {
 //              sh 'docker rmi  $(docker images -q)'
 //                  }
 //               }
 //             }
 //
 // stage('Deploy On Prod') {
 //     steps{
 //       sshagent(['ec2-user-password-credentials']) {
 //            sh "scp -o StrictHostKeyChecking=no docker-compose.yml ec2-user@18.219.210.241:"
 //            sh "ssh -o StrictHostKeyChecking=no ec2-user@18.219.210.241 docker-compose up -d"
 //           }
 //         }
 //      }
 //
 //  stage('Remove images from Agent Server') {
 //        steps{
 //            script {
 //                sh 'docker rmi  $(docker images -q)'
 //                  }
 //              }
 //            }
 //
 //  stage('Remove ps from Agent Server') {
 //        steps {
 //              sh 'docker ps -f name=framed -q | xargs --no-run-if-empty docker container stop'
 //              sh 'docker container ls -a -fname=framed  -q | xargs -r docker container rm'
 //              sh 'docker container ls '
 //                }
 //            }

   }
}
