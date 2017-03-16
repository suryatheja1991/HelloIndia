node {
   def mvnHome
   def version 
   stage('Preparation') {
      git 'https://github.com/SeshagiriSriram/addressbook.git'
      mvnHome = tool 'LOCAL_MAVEN'
	  version = '2.3.5' 
   }
   stage('PerformUnitTest') {
        withMaven(
        maven: 'LOCAL_MAVEN', // Maven installation declared in the Jenkins "Global Tool Configuration"
        mavenSettingsConfig: 'settings.xml', // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        mavenLocalRepo: 'd:/repos') {

      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean test"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean test/)
      }
    } // withMaven will discover the generated Maven artifacts, JUnit reports and FindBugs reports
    

   }
   stage('PublishResults') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }

   stage('NotifySachinandCo') { 
   } 
} 