pipeline {
     agent any
     stages {
         
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e ./app/*.html'
              }
         }

         stage('Upload Docker') {
             steps {

                 println(hudson.util.Secret.fromString("{PASSWORD}").getPlainText())
                 
                 dir("$WORKSPACE")
                 {
                    script{


def DOCKER_REGISTRY_URI="https://hub.docker.com/repository/docker/tamermohamed/udacity_capstone"

withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'username', passwordVariable: 'passwordVariable')]) {


                    docker.withRegistry('https://hub.docker.com/repository/docker/tamermohamed', 'dockerhub') {

                        def udacity_capstone_image = docker.build("udacity_capstone:v1.0")
                        sh "echo ${usernameVariable}"
                        sh "docker login -u ${usernameVariable} -p ${passwordVariable}"

                        udacity_capstone_image.push()
   
                    }

}
                 }
             }
         }
         }


         stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName: 'tamermohamed/udacity_capstone:v1.0', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
              }
         } 

         // stage('Upload to AWS') {
         //      steps {
         //          withAWS(region:'us-east-2',credentials:'aws-static') {
         //          sh 'echo "Uploading content with AWS creds"'
         //              s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-pipeline')
         //          }
         //      }
         // }
     }
}