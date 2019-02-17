node {
  stage('SCM') {
    git 'https://github.com/eugenmorar/cucumberbasic.git'
  }
  stage('SonarQube analysis') {
    withSonarQubeEnv('LocalSonarServer') {
      sh 'mvn clean package sonar:sonar'
    } // SonarQube taskId is automatically attached to the pipeline context
  }
}
