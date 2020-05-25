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



                          withCredentials([
            usernamePassword(credentialsId: 'dockerhub',
              usernameVariable: 'username',
              passwordVariable: 'password')
          ]) {


            sh "docker login -u ${username} -p ${password}"
            sh "docker tag udacity_capstone tamermohamed/udacity_capstone:v1.0"
            sh "docker push tamermohamed/udacity_capstone:v1.0"

            

            // print 'username=' + username + 'password=' + password

            // print 'username.collect {it} =' + (username.collect { it }).join('')
           
          }




// def DOCKER_REGISTRY_URI="https://hub.docker.com/repository/docker/tamermohamed/udacity_capstone"
// withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'username', passwordVariable: 'passwordVariable')]) {
// sh  "echo username= ${username} , password= ${password}"

// }

// withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'username', passwordVariable: 'passwordVariable')]) {

//                     sh  "echo username= ${username} , password= ${password}"
//                     // docker.withRegistry('https://hub.docker.com/repository/docker/tamermohamed', 'dockerhub') {

//                     //     def udacity_capstone_image = docker.build("udacity_capstone:v1.0")
                       
//                     //     sh "docker login -u ${username} -p ${password}"

//                     //     udacity_capstone_image.push()
   
//                     // }

// }
                 }
             }
         }
         }


        //  stage('Security Scan') {
        //       steps { 
        //          aquaMicroscanner imageName: 'tamermohamed/udacity_capstone:v1.0', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
        //       }
        //  } 

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