node {

    def mvnHome = tool name: "demo-maven:3.8.6"
    stage ("checkout")  {
       checkout([$class: 'GitSCM', branches: [[name: '*/custom-pom-mpm']], extensions: [], userRemoteConfigs: [[credentialsId: 'democalculus_github_creds_ID', url: 'https://github.com/democalculus/maven-web-application.git']]])
    }

   stage ('build')  {
    sh "${mvnHome}/bin/mvn  clean install -f maven-web-app/pom.xml"
    }

     stage ('Code Quality scan')  {
       withSonarQubeEnv('sonar_creds') {
       sh "${mvnHome}/bin/mvn -f maven-web-app/pom.xml sonar:sonar"
        }
   }

   stage ('Code coverage always successful')  {
          //jacoco()
          jacoco deltaBranchCoverage: '80', deltaClassCoverage: '80', deltaComplexityCoverage: '80', deltaInstructionCoverage: '80', deltaLineCoverage: '80', deltaMethodCoverage: '80', maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
       }
   stage ('Nexus upload')  {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '34.125.253.100:8081',
        groupId: 'custom-pom',
        version: '1.0-SNAPSHOT',
        repository: 'demo-walmart-snapshop',
        credentialsId: 'nexus_creds_id',
        artifacts: [
            [artifactId: 'maven-web-app',
             classifier: '',
             file: 'maven-web-app/target/maven-web-app.war',
             type: 'war']
        ]
     )
    }
stage ('Code coverage always successful')  {
        jacoco( jacoco buildOverBuild: true, changeBuildStatus: true, deltaBranchCoverage: '80', deltaClassCoverage: '80', deltaComplexityCoverage: '80', deltaInstructionCoverage: '80', deltaLineCoverage: '80', deltaMethodCoverage: '80', maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80',            minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
         )
        }
//    stage ('DEV Deploy')  {
//       echo "deploying to DEV Env "
//       deploy adapters: [tomcat9(credentialsId: '4c55fae1-a02d-4b82-ba34-d262176eeb46', path: '', url: 'http://your_tomcat_url:8080')], contextPath: null, war: '**/*.war'
//
//     }
//
  stage ('Slack notification')  {
    slackSend(channel:'multibranch_notification', message: "Job is successful, here is the info -  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
   }

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
}
