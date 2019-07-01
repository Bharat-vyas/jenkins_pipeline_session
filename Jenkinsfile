node {
      stage('Scm Checkout'){
            checkout scm
           // sh "echo $BRANCH_NAME"
           echo 'BUILD_URL is ---' +env.BUILD_URL
           echo 'JOB_URL is -----' +env.JOB_URL
           echo 'WORKSPACE is ---' +env.WORKSPACE
           echo 'JOB NAME is ----' +env.JOB_NAME
           echo 'JOB Base NAME is ----' +env.JOB_BASE_NAME
           command = "echo $JOB_NAME | cut -d '/' -f1"
            echo 'auto_back' +env.command
            //  echo env.command;
           // echo command;
          // echo 'auto_back_' +env.command
          //  echo 'auto_back_'${env.command}
           // sh "ls -al /var/lib/jenkins"
           // git branch: 'bharat', url: 'https://github.com/Bharat-vyas/jenkins_pipeline_session.git'      
      //git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
      
   /* stage ('Build Web Image')
    {
    sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
          def image1 = docker.build bharatvyas/jenkins_demo:${env.BUILD_ID}", "--file docker/Dockerfile .")
    }
      
    stage('Push image to dockerhub'){
    withDockerRegistry(credentialsId: 'dockerhub') {
       sh "docker push bharatvyas/jenkins_demo:${env.BUILD_ID}"
       image1.push()
     }
    }*/
      if (env.BRANCH_NAME == 'master')
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
                  // NEXUS_URL = 'https://mynexus.com'
                  // REPONAME    = 'myrepo'
                  
                  //echo env.NEXUS_URL + env.REPONAME
                  sshCommand remote: remote, command: "pwd"
                  sshCommand remote: remote, command: "ls -al /home/test"
                  sshCommand remote: remote, command: "tar -cvf /home/${env.BUILD_ID}.tar /home/test"
                  sshCommand remote: remote, command: "rm -rf /home/test"
                  sshCommand remote: remote, command: "git clone -b bharat https://github.com/Bharat-vyas/jenkins_pipeline_session.git /home/test" 
                  sshCommand remote: remote, command: "ls -al /home/test"
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
