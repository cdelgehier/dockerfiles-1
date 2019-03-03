pipeline {
  agent any
  environment {
    PYTHONUNBUFFERED = '1'
    ANSIBLE_FORCE_COLOR = 'true'
  }
  parameters {
    choice(name: 'SDS_RELEASE', choices: ['18.10', '18.04'], description: 'Openio release')
    booleanParam(name: 'LATEST', defaultValue: false, description: 'Latest version ?')
  }
  stages {
    stage('build') {
      steps {
        dir("deployment/sds") {
          sh './build.sh'
        }
      }
    }
  }
  post {
    always {
      // delete workspace
      cleanWs()
    }
  }
}
