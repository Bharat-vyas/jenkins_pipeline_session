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
          sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile1 ."
          //def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile .")
          }
          catch(e)
          {
          build_ok = false
          echo e.toString()  
          }
        
          sh  "docker build -t bharatvyas/jenkins_demo:12 -f docker/Dockerfile ."
          
    }
      
      stage ('echo hello')
            {
                  sh "echo hello"
            }
      
      stage ('new stage')
      {
      sh  "docker build -t bharatvyas/jenkins_demo:13 -f docker/Dockerfile ."
      }

      if(build_ok) {
        currentBuild.result = "SUCCESS"
    } else {
        currentBuild.result = "FAILURE"
    }
      
} //node end
