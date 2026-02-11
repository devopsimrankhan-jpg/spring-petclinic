pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('jenkins-token')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/devopsimrankhan-jpg/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('SonarCloud Scan') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.projectKey=devopsimrankhan-jpg_spring-petclinic \
                    -Dsonar.organization=devopsimrankhan-jpg \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
    }
}
