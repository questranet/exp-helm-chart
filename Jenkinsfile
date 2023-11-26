pipeline {

  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Choose Environment')
    choice(name: 'APP_NAME', choices: ['backend', 'frontend'], description: 'Choose AppName')
    string(name: 'VERSION', defaultValue: '', description: 'Version to Deploy')
  }

  stages {

    stage('Deployment') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/questranet/${APP_NAME}'
        }
        sh 'helm upgrade -i ${APP_NAME} . -f APP/helm/${ENV}.yaml --set appVersion=${VERSION}'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}