pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        dir(path: "openio-sds/${SDS_RELEASE}/centos/7") {
          sh "pwd"
          sh "echo ${SDS_RELEASE}"
          sh "./build.sh"
        }

      }
    }
  }
  environment {
    PYTHONUNBUFFERED = '1'
    ANSIBLE_FORCE_COLOR = 'true'
  }
  post {
    always {
      cleanWs()

    }

  }
  parameters {
    choice(name: 'SDS_RELEASE', choices: ['18.10', '18.04'], description: 'Openio release')
    booleanParam(name: 'LATEST', defaultValue: false, description: 'Latest version ?')
  }
}
