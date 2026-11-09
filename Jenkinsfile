
pipeline {
    agent any

    tools {
        jdk 'JDK_21'
        maven 'Maven_3_8_4'
    }

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        SONAR_PROJECT_KEY = 'souravbuggywebapp'
        SONAR_ORGANIZATION = 'souravbuggywebapp'
        SONAR_HOST_URL = 'https://sonarcloud.io'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub.'
                sh 'git log -1 --oneline'
            }
        }

        stage('Compile and Build') {
            steps {
                echo 'Starting Maven compilation and build...'

                sh 'mvn clean verify'
            }
        }

        
        stage('SonarCloud Analysis') {
            steps {
                echo 'Starting SonarCloud analysis...'
        
                withCredentials([
                    string(
                        credentialsId: 'sonarcloud-token',
                        variable: 'SONAR_TOKEN'
                    )
                ]) {
                    sh '''
                        mvn org.sonarsource.scanner.maven:sonar-maven-plugin:5.8.0.7211:sonar \
                        -Dsonar.projectKey=souravbuggywebapp \
                        -Dsonar.organization=souravbuggywebapp \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.token="$SONAR_TOKEN" \
                        -Dsonar.nodejs.executable=/usr/bin/node-22
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '''
            ==========================================
            PIPELINE EXECUTION SUCCESSFUL!
            Maven Build: SUCCESS
            SonarCloud Analysis: SUCCESS
            ==========================================
            '''
        }

        failure {
            echo '''
            ==========================================
            PIPELINE EXECUTION FAILED!
            Please check the failed stage in Console Output.
            ==========================================
            '''
        }

        always {
            echo 'DevSecOps CI pipeline execution completed.'
        }
    }
}
