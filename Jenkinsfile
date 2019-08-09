node {
      stage('Scm Checkout'){
            checkout scm
            sh "echo $BRANCH_NAME"
       }
      
    stage ('Build Web Image')
    {       
          try {
          sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
          //def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile .")
            }
          finally {
          sh  "docker build -t bharatvyas/jenkins_demo:1 -f docker/Dockerfile ."
          }
          
    }
      


} //node end
