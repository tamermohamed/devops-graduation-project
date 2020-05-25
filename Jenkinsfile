pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    stage('Upload Docker') {
      steps {
        dir(path: "$WORKSPACE") {
          script {
            docker.withRegistry('https://hub.docker.com/', 'dockerhub') {

              def udacity_capstone_image = docker.build("udacity_capstone:v1.0")

              udacity_capstone_image.push()

            }
          }

        }

      }
    }

    stage('Security Scan') {
      steps {
        aquaMicroscanner(imageName: 'tamermohamed/udacity_capstone:v1.0', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html')
      }
    }

  }
}