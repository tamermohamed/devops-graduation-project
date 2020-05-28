pipeline {
     agent any
     stages {
         
         stage('Lint') {
              steps {
                  sh 'tidy -q -e ./app/*.html'
              }
         }

        //  stage('Upload Docker') {
        //      steps {

                
                 
        //          dir("$WORKSPACE")
        //          {
        //             script{



        //                   withCredentials([
        //     usernamePassword(credentialsId: 'dockerhub',
        //       usernameVariable: 'username',
        //       passwordVariable: 'password')
        //   ]) {

        //     docker.build("udacity_capstone")
        //     sh "docker login -u ${username} -p ${password}"
        //     sh "docker tag udacity_capstone tamermohamed/udacity_capstone:v1.0"
        //     sh "docker push tamermohamed/udacity_capstone:v1.0"

        //   }


        //          }
        //      }
        //  }
        //  }


// stage('Test EKS Deploy') {
//             steps {
//                 dir('kubernetes') {
//                     withAWS(credentials: 'eks', region: 'us-west-2') {

//                         sh '''
//                         /home/ubuntu/.local/bin/aws eks --region us-west-2 update-kubeconfig --name production
//                         kubectl apply -f deployment.yaml
//                         kubectl apply -f service.yaml

//                         '''
                           
//                         }
//                     }
//             }
//         }

stage('deploy cluster')
{
    steps{
        dir('')
        {
            kubernetesDeploy(kubeconfigId: 'kube', configs: 'deployment.yaml', enableConfigSubstitution: true)        
        }
    }
}
         stage('EKS Deploy') {
            steps {
                dir('kubernetes') {
                    withAWS(credentials: 'eks', region: 'us-west-2') {

                        sh '''
                        
                        kubectl apply -f deployment.yaml
                        kubectl apply -f service.yaml

                        '''
                           
                        }
                    }
            }
        }



     }
}