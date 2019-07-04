node {
      stage('Scm Checkout')
      {
            checkout scm
            sh "tar -cvf workspace.tar ."
      }
     
     if (env.BRANCH_NAME == 'bharat')
{
 
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
                  webpath = '/home/test'
                  sshCommand remote: remote, command: "tar -cvf /home/auto_back_${env.BUILD_ID}.tar /home/test"
                  sshCommand remote: remote, command: "rm -rf /home/test/; mkdir /home/test"
                  sshPut remote: remote, from: 'workspace.tar', into: "${webpath}"
                  sshCommand remote: remote, command: "tar -xvf ${webpath}/workspace.tar -C ${webpath}; rm -rf ${webpath}/workspace.tar"
            } 
     
     
}     
} //if condition end      
}//node end
