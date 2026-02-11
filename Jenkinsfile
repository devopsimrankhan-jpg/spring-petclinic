pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=devopsimrankhan-jpg_spring-petclinic \
                    -Dsonar.organization=devopsimrankhan-jpg \
                    -Dsonar.host.url=https://sonarcloud.io
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
