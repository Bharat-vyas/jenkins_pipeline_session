node {
      def build_ok = true
      stage('Scm Checkout'){
            checkout scm
            sh "echo $BRANCH_NAME"
       }         
    stage ('Build Web Image')
    {         
          try {
          echo "===================================HELLO==================================="
                // We have define Dockerfile1 at the end that's why it always fails and then we will handle the error using 
                // catch statement which will alter the result from failure to success
          sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile1 ."
          //def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile1 .")
          }
          
          catch (Exception o) 
          {
           currentBuild.result = 'SUCCESS'
         // currentBuild.result = 'FAILURE'      //"also test with FAILURE"
           sh  "docker build -t bharatvyas/jenkins_demo:11 -f docker/Dockerfile ."
          }
          
          echo "RESULT: ${currentBuild.result}"
          sh  "docker build -t bharatvyas/jenkins_demo:12 -f docker/Dockerfile ."
    }
      
      stage ('new stage')
      {
      sh  "docker build -t bharatvyas/jenkins_demo:13 -f docker/Dockerfile1 ."
      }

      stage ('echo hello')
      {
      sh "echo hello"
      }
} //node end
