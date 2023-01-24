pipeline {
  agent { label 'maven' }

  environment {
    DOCKER_TARGET = 'ghcr.io/e-learning-by-sse/infrastructure-fake-oidc'
  }
  
  stages {
    
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
            version = sh(
                returnStdout: true,
                script: "mvn org.apache.maven.plugins:maven-help-plugin:3.2.0:evaluate -Dexpression=project.version -q -DforceStdout")
              .trim()
            image = docker.image("${env.DOCKER_TARGET}")
            docker.withRegistry('https://ghcr.io', 'github-ssejenkins') {
              image.push("${version}")
              image.push('latest')
            }
          }
      }
    }
  }
}
