node {
      stage('Scm Checkout'){
            checkout scm
            sh "echo $BRANCH_NAME"
           // git branch: 'bharat', url: 'https://github.com/Bharat-vyas/jenkins_pipeline_session.git'      
      //git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
      
   
      if (env.BRANCH_NAME == 'latest')
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
            sshCommand remote: remote, command: "pwd"
            sshCommand remote: remote, command: "cd /home/test; ls -al"
 
                  def exists = fileExists '/home/test/Jenkinsfile'

                  if (fileExists('/home/test/Jenkinsfile')) {
                        echo 'Yes'
                  } 
                  else {
                        sh "pwd"
                        echo 'No'
                  }
                  
            //sshCommand remote: remote, command: "git clone -b bharat https://github.com/Bharat-vyas/jenkins_pipeline_session.git /home/test" 
            //sshCommand remote: remote, command: "cd ~/jenkins_pipeline_demo_bharat; ls -al"
            } 
     
            
      
      
      

}     
} //if condition end      
} //node end
