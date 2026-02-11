pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarCloud Scan') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh '''
                    mvn clean verify sonar:sonar \
                      -Dsonar.projectKey=devopsimrankhan_spring-petclinic \
                      -Dsonar.organization=devopsimrankhan \
                      -Dsonar.host.url=https://sonarcloud.io
                    '''
                }
            }
        }

        stage("Quality Gate") {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
