pipeline {
  agent { label 'maven' }

  stages {
    stage ('Maven') {
      steps {
        script {
          withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
            docker.withRegistry('https://ghcr.io', 'github-ssejenkins') {
              sh 'mvn spring-boot:build-image -Dspring-boot.build-image.imageName=ghcr.io/e-learning-by-sse/infrastructure-fake-oidc:latest'
            }
          } 
        }
      }
    }
  }
}
