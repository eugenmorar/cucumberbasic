node {
  stage('SCM') {
    git 'https://github.com/eugenmorar/cucumberbasic.git'
  }
  stage('Sonar analysis') {
    withSonarQubeEnv('LocalSonarServer') {
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
    } // SonarQube taskId is automatically attached to the pipeline context
  }
}
