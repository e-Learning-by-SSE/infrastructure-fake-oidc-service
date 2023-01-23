pipeline {
  agent { label 'maven' }

  stages {
    stage ('Maven') {
      steps {
        configFileProvider([configFile(fileId: "elearn-docker-settings", variable: 'dockerConfigFile')]) {
          sh "source $dockerConfigFile && export DOCKER_REPO_PATH"
        }
        //withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
        //}
      }
    }
  }
}
