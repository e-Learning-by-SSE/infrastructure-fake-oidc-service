pipeline {
  agent { label 'maven' }
  stages {
    stage ('Maven') {
      environment {
        DOCKER_TARGET = 'ghcr.io/e-learning-by-sse/infrastructure-fake-oidc'
      }
      steps {
        sh 'mvn spring-boot:build-image -Dspring-boot.build-image.imageName=${env.DOCKER_TARGET}'
        script {
          image = docker.image(${env.DOCKER_TARGET})
          docker.withRegistry('https://ghcr.io', 'github-ssejenkins') {
            image.push()
            image.push('latest')
          }
        }
      }
    }
  }
}
