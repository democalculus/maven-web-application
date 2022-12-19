# maven-web-application
#walmart-dev-mss branch added   Dec_91_22
#configure nexus details in jenkins
#contextPath
#/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/demo-maven_3.8.6/conf
<server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
#where to past it
-->
    <server>
      <id>nexus</id>
      <username>admin</username>
      <password>passw0rd</password>
    </server>
  </servers>

  <!-- mirrors
