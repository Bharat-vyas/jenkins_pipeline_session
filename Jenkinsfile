node {
      stage('Scm Checkout'){
            checkout scm
      //git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
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
      if (env.BRANCH_NAME == 'bharat')
{
// 
withCredentials([usernamePassword(credentialsId: 'jenkins_pipeline_demo_kishortest_localserver', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')])
{ 
  def remote = [:]
  remote.name = 'VM'
  remote.host = '172.16.16.70'
  remote.user = "${USERNAME}"
  remote.password = "${PASSWORD}"
  remote.allowAnyHosts = true

      stage('Pull image and create container') 
      {
                  withDockerRegistry(credentialsId: 'dockerhub') 
                  {
                        //sshCommand remote: remote, command: "hostname ; docker pull bharatvyas/jenkins_demo:${env.BUILD_ID} ; docker images"
                  //sh "docker pull bharatvyas/jenkins_demo:${env.BUILD_ID}"
                  //sh "docker logout"
                  }     
      }
}
} //if condition end
      
} //node end
