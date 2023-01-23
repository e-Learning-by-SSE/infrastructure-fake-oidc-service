pipeline {
  agent { label 'maven' }

  stages {
    stage ('Maven') {
      steps {
        configFileProvider(
          [configFile(fileId: "elearn-docker-settings", variable: 'DOCKER_CONFIG')]) {
          sh ". $DOCKER_CONFIG"
          sh 'echo $DOCKER_REPO_PATH'
          sh "printenv"
        }
        //withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
        //}
      }
    }
  }
}
