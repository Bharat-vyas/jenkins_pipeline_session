node {
      stage('Scm Checkout'){
      git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
      
    stage ('Build Web Image')
    {
    sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
    }
      
    stage('Push image to dockerhub'){
    withDockerRegistry(credentialsId: '996ea76f-df01-4824-9db3-0bc3a7c24c21'){
            sh 'docker push bharatvyas/jenkins_demo:${env.BUILD_ID}'
      }
    }
}
