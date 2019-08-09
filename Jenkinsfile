node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git branch: 'i1-modify-for-qTest', url: 'https://github.com/SouLeader/Java-Junit-Selenium.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.5.2'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -f pom.xml -Dmaven.test.failure.ignore clean test"
      } else {
         bat(/"${mvnHome}\bin\mvn" -f pom.xml -Dmaven.test.failure.ignore clean test/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   stage('qTestJenkinsPlugin'){
       submitJUnitTestResultsToqTest([apiKey: '15cd90d5-53c5-4d8b-a292-823ba5a18fd7', containerID: 563934, containerType: 'release', createTestCaseForEachJUnitTestClass: true, createTestCaseForEachJUnitTestMethod: false, environmentID: 54436, overwriteExistingTestSteps: true, parseTestResultsFromTestingTools: true, parseTestResultsPattern: 'target/**/**.xml', projectID: 203648, qtestURL: 'https://qteststaging3.staging.qtestnet.com', submitToAReleaseAsSettingFromQtest: true, submitToExistingContainer: false, utilizeTestResultsFromCITool: false])
   }
}
