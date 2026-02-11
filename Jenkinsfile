pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=devopsimrankhan-jpg_spring-petclinic \
                        -Dsonar.organization=devopsimrankhan-jpg \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.branch.name=main
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
