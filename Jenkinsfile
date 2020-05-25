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
                 dir("$WORKSPACE")
                 {
                    script{

withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {

    
                    docker.withRegistry('index.docker.io', 'dockerhub') {

                        def udacity_capstone_image = docker.build("udacity_capstone:v1.0")

                        sh "docker login -u ${USERNAME} -p ${PASSWORD}"

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