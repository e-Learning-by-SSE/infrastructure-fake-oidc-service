pipeline {
  agent { label 'maven' }

  stages {
    environment {
      DOCKER_TARGET = 'ghcr.io/e-learning-by-sse/infrastructure-fake-oidc'
    }
    stage ('Maven') {
      steps {
        withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
          sh 'mvn spring-boot:build-image -Dspring-boot.build-image.imageName=${env.DOCKER_TARGET}'
        }
      }
    }
    stage ('Publish') {
      steps {
        script {
            image = docker.image("${env.DOCKER_TARGET}")
            version = env.API_VERSION = sh(
                returnStdout: true,
                script: 'mvn -q -Dexec.executable=echo -Dexec.args='${project.version}' --non-recursive exec:exec')
              .trim()
            docker.withRegistry('https://ghcr.io', 'github-ssejenkins') {
              image.push("${version}")
              image.push('latest')
            }
          }
      }
    }
  }
}
