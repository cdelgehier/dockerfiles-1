pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        dir(path: "openio-sds/${SDS_RELEASE}/centos/7") {
          sh 'pwd'
          sh "echo ${SDS_RELEASE}"
          sh './build.sh'
        }

      }
    }
    stage('docker push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'ID_HUB_DOCKER', usernameVariable: 'docker_user', passwordVariable: 'docker_pass')]) {
              sh "echo \${docker_pass} | docker login --password-stdin -u \${docker_user}"
            }
        script {
          sh "docker push openio/sds:${SDS_RELEASE}"

          if (params.LATEST) {
            sh "docker tag openio/sds:${SDS_RELEASE} openio/sds:latest"
            sh "docker push openio/sds:latest"

          }
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
