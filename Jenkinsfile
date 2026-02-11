stage('SonarCloud Scan') {
    steps {
        withSonarQubeEnv('SonarCloud') {
            sh '''
            mvn sonar:sonar \
              -Dsonar.projectKey=your_project_key \
              -Dsonar.organization=your_org \
              -Dsonar.host.url=https://sonarcloud.io
            '''
        }
    }
}
