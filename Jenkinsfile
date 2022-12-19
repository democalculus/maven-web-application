node {

    def mvnHome = tool name: "demo-maven:3.8.6"
    stage ("checkout")  {
       checkout([$class: 'GitSCM', branches: [[name: '*/walmart-dev-mss']], extensions: [], userRemoteConfigs: [[credentialsId: 'democalculus_github_creds_ID', url: 'https://github.com/democalculus/maven-web-application.git']]])
    }

   stage ('build')  {
    sh "${mvnHome}/bin/mvn  clean package"
    }

     stage ('Code Quality scan')  {
       withSonarQubeEnv('sonar_creds') {
       sh "${mvnHome}/bin/mvn clean package sonar:sonar"
        }
   }

   stage ('Code coverage')  {
          jacoco()
       }

   stage ('Nexus upload')  {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: 'http://34.125.253.100:8081',
        groupId: 'com.mt',
        version: '1.0-SNAPSHOT',
        repository: 'eagunu-mvn-snapshot-mss',
        credentialsId: 'nexus_creds_id',
        artifacts: [
            [artifactId: 'maven-web-app',
             classifier: '',
             file: 'Dashboard/maven project/walmart-dev-mss/target/maven-web-app.war',
             type: 'war']
        ]
     )
    }
}
//    stage ('DEV Deploy')  {
//       echo "deploying to DEV Env "
//       deploy adapters: [tomcat9(credentialsId: '4c55fae1-a02d-4b82-ba34-d262176eeb46', path: '', url: 'http://your_tomcat_url:8080')], contextPath: null, war: '**/*.war'
//
//     }
//
//   stage ('Slack notification')  {
//     slackSend(channel:'channel-name', message: "Job is successful, here is the info -  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
//    }
//
//    stage ('DEV Approve')  {
//             echo "Taking approval from DEV Manager for QA Deployment"
//             timeout(time: 7, unit: 'DAYS') {
//             input message: 'Do you approve QA Deployment?', submitter: 'admin'
//             }
//      }
//
// stage ('QA Deploy')  {
//      echo "deploying into QA Env "
// deploy adapters: [tomcat9(credentialsId: '4c55fae1-a02d-4b82-ba34-d262176eeb46', path: '', url: 'http://your_tomcat_url:8080')], contextPath: null, war: '**/*.war'
//
// }
//
//
//   stage ('QA notify')  {
//     slackSend(channel:'channel-name', message: "QA Deployment was successful, here is the info -  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
//    }
//
// stage ('QA Approve')  {
//     echo "Taking approval from QA manager"
//     timeout(time: 7, unit: 'DAYS') {
//         input message: 'Do you want to proceed to PROD Deploy?', submitter: 'admin,manager_userid'
//   }
// }
//
// stage ('PROD Deploy')  {
//      echo "deploying into PROD Env "
// deploy adapters: [tomcat9(credentialsId: '4c55fae1-a02d-4b82-ba34-d262176eeb46', path: '', url: 'http://your_tomcat_url:8080')], contextPath: null, war: '**/*.war'
//
 // }
// }
