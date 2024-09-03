node {
   // Set up tools
   def mvnHome = tool 'M3'
   def jdkHome = tool name: 'jdk1.8.0_202', type: 'hudson.model.JDK'

   // Set JAVA_HOME environment variable
   env.JAVA_HOME = jdkHome
   env.PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
   
   stage('Checkout Code') { 
      git 'https://github.com/rickytang681/SCC-AssignmentII-java-maven-calculator-web-app.git'
   }
   stage('JUnit Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' clean test"
      } else {
         bat(/"${mvnHome}\bin\mvn" clean test/)
      }
   }
   stage('Integration Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' integration-test"
      } else {
         bat(/"${mvnHome}\bin\mvn" integration-test/)
      }
   }
 /*
   stage('Performance Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' cargo:start verify cargo:stop"
      } else {
         bat(/"${mvnHome}\bin\mvn" cargo:start verify cargo:stop/)
      }
   }
  */
  stage('Performance Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' verify"
      } else {
         bat(/"${mvnHome}\bin\mvn" verify/)
      }
   }
   stage('Deploy') {
      timeout(time: 10, unit: 'MINUTES') {
           input message: 'Deploy this web app to production ?'
      }
      echo 'Deploy...'
   }
}
   
