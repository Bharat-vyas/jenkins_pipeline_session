node {
      stage('Scm Checkout'){
      git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
      
    stage ('Build Web Image')
    {
    sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
    }
      
    stage('Push image to dockerhub'){
    withDockerRegistry(credentialsId: 'dockerhub') {
       sh "docker push bharatvyas/jenkins_demo:${env.BUILD_ID}"
      }
    }
   sshagent(['DrinkSavvy_AWS_TEST']) {
    sh "hostname"
    }  
}
