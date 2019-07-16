node {
    stage ('Checkout'){
	    checkout scm
        sh "tar -cvf boothkicker_latest.tar ."
    }

	withCredentials([usernamePassword(credentialsId: 'QAMAC', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
      def remote = [:]
      remote.name = 'mac'
      remote.host = '172.16.16.221'
      remote.user = "${USERNAME}"
      remote.password = "${PASSWORD}"
      remote.allowAnyHosts = true
		
		 stage('Run Katalon test')
            {
		     sshCommand remote: remote, command: "ls; hostname" 
		     sshCommand remote: remote, command: "cd "
	    }
	}
	
	
	
	
         if (env.BRANCH_NAME == 'release')
      {
      // 
      withCredentials( [usernamePassword( credentialsId: 'kishortest', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
      {
      def remote = [:]
      remote.name = 'boothkicker_web'
      remote.host = '165.22.34.169'
      remote.user = "${USERNAME}"
      remote.password = "${PASSWORD}"
      remote.allowAnyHosts = true
          
            stage('Backup and remove the older code base')
            {
                  webpath = '/usr/share/nginx/html'
                  sshCommand remote: remote, command: "cd ${webpath}; tar -cvf web_auto_back/backup_${env.BUILD_ID}.tar boothkicker-web; cd web_auto_back; ls -1tr | head -n -4 | xargs -d '\n' rm -f --"  // the last command is to make sure that there will be maximum only 4 backup.tar files (only 4 latest tar files will be kept and older then 4 will get deleted automatically) 
                  //sshCommand remote: remote, command: "tar -cvf /usr/share/nginx/html/web_auto_back_${env.BUILD_ID}.tar /usr/share/nginx/html/boothkicker-web"
                  sshCommand remote: remote, command: "rm -rf ${webpath}/boothkicker-web; mkdir ${webpath}/boothkicker-web"
            }      
            
            stage('Update with latest code base')
            {     
                  sshPut remote: remote, from: 'boothkicker_latest.tar', into: "${webpath}/"
                  sshCommand remote: remote, command: "tar -xvf ${webpath}/boothkicker_latest.tar -C ${webpath}/boothkicker-web; rm -rf ${webpath}/boothkicker_latest.tar"
            } 
       } //
       } // If statement close
}    // Node End
