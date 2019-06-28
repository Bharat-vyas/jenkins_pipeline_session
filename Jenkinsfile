node {
      stage('Scm Checkout'){
            checkout scm
            sh "echo $BRANCH_NAME"
      //git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
      
    stage ('Build Web Image')
    {
    sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
          //def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile .")
    }
      
    //stage('Push image to dockerhub'){
    //withDockerRegistry(credentialsId: 'dockerhub') {
    //   sh "docker push bharatvyas/jenkins_demo:${env.BUILD_ID}"
     //  image1.push()
      //}
    //}
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

      
          
            stage('execute commands')
            {
            sshCommand remote: remote, command: "cd /home/test; ls -al"
            sshCommand remote: remote, command: "git clone https://github.com/Bharat-vyas/jenkins_pipeline_session.git" 
            
                  //checkout([$class: 'GitSCM', branches: [[name: '*/bharat']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://github.com/Bharat-vyas/jenkins_pipeline_session.git']]])
            sshCommand remote: remote, command: "cd /home/test; ls -al"
            } 
     
            
      
      
      /*stage('Pull image and create container') 
      {                     
                  withDockerRegistry(credentialsId: 'dockerhub') 
                  {
                        sshCommand remote: remote, command: "hostname ; docker pull bharatvyas/jenkins_demo:${env.BUILD_ID}; docker logout; docker images; docker run -itd -p 8181:80 bharatvyas/jenkins_demo:${env.BUILD_ID}; docker ps"
                        //sshCommand remote: remote, command: "hostname ; docker pull bharatvyas/jenkins_demo:${env.BUILD_ID}; docker logout; docker images; docker ps"
                        
                        //sh "docker pull bharatvyas/jenkins_demo:${env.BUILD_ID}"
                  }     
      }*/

}     
} //if condition end      
} //node end
