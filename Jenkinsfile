pipeline {
  agent any
  tools { 
        maven 'Maven_3_8_4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=souravbuggywebapp -Dsonar.organization=souravbuggywebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=cdac1ae935f60b098d98d0a94f99d591b1958fd4'
			}
        }
  }
}
