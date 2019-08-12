node {
      stage('Scm Checkout'){
            checkout scm
            sh "echo $BRANCH_NAME"
       }
      
    stage ('Build Web Image')
    {       
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          echo "===================================HELLO==================================="
          sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
          //def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile .")
          }
        
          sh  "docker build -t bharatvyas/jenkins_demo:12 -f docker/Dockerfile ."
          
    }
      
      stage ('echo hello')
            {
                  sh "echo hello"
            }
      
      stage ('new image')
      {
             sh  "docker build -t bharatvyas/jenkins_demo:13 -f docker/Dockerfile ."
      }

} //node end
