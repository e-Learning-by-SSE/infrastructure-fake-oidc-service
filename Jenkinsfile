pipeline {
  agent { label 'maven' }

  stages {
    stage ('Maven') {
      steps {
        configFileProvider([configFile(fileId: "e-learn-docker-env", variable: 'dockerConfigFile')] {
          sh "source $dockerConfigFile && echo $DOCKER_REPO_PATH"
        }
        //withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
        //}
      }
    }
  }
}
