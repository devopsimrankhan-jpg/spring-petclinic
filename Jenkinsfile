pipeline {
  agent any

  environment {
    SONAR_TOKEN = credentials('jenkins-token2')
    SONAR_ORG = 'devopsimrankhan-jpg'
    SONAR_PROJECT_KEY = 'devopsimrankhan-jpg_spring-petclinic'
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean verify'
      }
    }

    stage('SonarCloud Scan') {
      steps {
        sh """
          mvn -B sonar:sonar \
            -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
            -Dsonar.organization=${SONAR_ORG} \
            -Dsonar.host.url=https://sonarcloud.io \
            -Dsonar.login=${SONAR_TOKEN}
        """
      }
    }
  }
}
