
pipeline {
    agent any

    tools {
        maven 'Maven_3_8_4'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Compile and Build') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'sonarcloud-token',
                        variable: 'SONAR_TOKEN'
                    )
                ]) {
                    sh '''
                        mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                        -Dsonar.projectKey=souravbuggywebapp \
                        -Dsonar.organization=souravbuggywebapp \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.token=$SONAR_TOKEN
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build and SonarCloud analysis completed successfully!'
        }

        failure {
            echo 'Pipeline execution failed. Check the console output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
