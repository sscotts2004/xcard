node('maven-label') {
   def mvnHome
   
  @Library('pipeline-library-demo')_
 stage("shared test library")
 {

  echo 'Hello World'

  sayHello 'Dave'

} 
   
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/sscotts2004/xcard.git'
      mvnHome = tool 'maven'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
