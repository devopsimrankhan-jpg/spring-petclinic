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
                withSonarQubeEnv('SonarQube-Cloud') {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=devopsimrankhan-jpg_spring-petclinic \
                    -Dsonar.organization=devopsimrankhan-jpg \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
