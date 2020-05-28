pipeline {
     agent any
     stages {
         
         stage('Lint') {
               steps
             {
                sh "tidy -q -e ./app/*.html"
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

            docker.build("udacity_capstone")
            sh "docker login -u ${username} -p ${password}"
            sh "docker tag udacity_capstone tamermohamed/udacity_capstone:v2.0"
            sh "docker push tamermohamed/udacity_capstone:v2.0"

          }


                 }
             }
         }
         }

stage('deploy v1 to eks')
{
    steps {
     dir('deployv1') {
            

                        sh '''
                        kubectl apply -f deployment.yml
                        kubectl apply -f service.yml
                        '''
                           
                        }
    }
                    
}
         
stage('deploy v2 to eks')
{
    steps {
     dir('deployv2') {
            

                        sh '''
                        kubectl apply -f deployment.yml
                        kubectl apply -f service.yml
                        '''
                           
                        }
    }
                    
}


     }
}