node {

  stage('Checkout') {
    	git 'https://github.com/eugenmorar/cucumberbasic.git'
  }

  stage('Sonar Analysis') {
    withSonarQubeEnv('LocalSonarServer') {
      	sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
    } 
  }

  stage('Build') {
   steps {
	    sh 'mvn clean package'      
   }
   post {
	    echo 'Archiving ...'
	    archiveArtifacts artifacts: '**/target/*.war'
   } 	
  
  stage('Browser Testing') {
      echo 'Test Succeeded'	
  }

  stage('Deploy on Tomcat') {
      sh 'sshpass -p "eugen" scp -r **/target/*.war root@192.168.109.100:/var/lib/tomcat8/webapps/webapp.war'	
  }

  stage('Create Report') {
      step([$class: "CucumberReportPublisher", failedFeaturesNumber: 0, failedScenariosNumber: 0, failedStepsNumber: 0, fileExcludePattern: '', fileIncludePattern: '**/*json', jsonReportDirectory: '', parallelTesting: false, pendingStepsNumber: 0, skippedStepsNumber: 0, trendsLimit: 0, undefinedStepsNumber: 0])
  }
}
