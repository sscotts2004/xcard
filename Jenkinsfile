@Library('pipeline-library-demo')_

def say(String name = 'human') {
  echo "Hello, ${name}."
  echo "Hello, ${name}."
}

node('maven-label') {
   def mvnHome
   
   stage('shard lib Demo') {

        echo 'Hello World'

        sayHello 'Dave'

}
   
   stage('reference lib Demo') {


        say 'Edureka'

}
   stage('Preparation') { // for display purposes
      
      git 'https://github.com/isandt/xcard.git'
             
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
  stage('Review') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' sonar:sonar -Dsonar.host.url='http://ec2-3-82-175-128.compute-1.amazonaws.com:9000'"
      } else {
         bat(/"${mvnHome}\bin\mvn" sonar:sonar/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
