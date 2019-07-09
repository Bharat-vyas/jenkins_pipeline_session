node {
    stage ('Checkout'){
	    checkout scm
        sh "tar -cvf boothkicker_latest.tar ."
    }

    stage('SonarQube analysis') {
	    // requires SonarQube Scanner 2.8+
	    def scannerHome = tool 'Sonar-Scanner';
	    withSonarQubeEnv('SonarQube') {
	      def projectKey=env.JOB_NAME.replaceAll('/','.')
	      sh "${scannerHome}/bin/sonar-scanner -D sonar.projectKey=${projectKey}  -D sonar.sources=. -D sonar.exclusions=app_data/**,assets/**,bootstrap/**,docker/**,mail/**,messages/**,migrations/**,runtime/**,test/**,vagrant/**,vendor/**,web/**,widgets/**"
		  stash includes: ".sonar/report-task.txt", name: 'sonar'
	    }
  }

  stage("Quality Gate"){
            unstash 'sonar'
            def props = getProperties(".sonar/report-task.txt")
            def sonarServerUrl=props.getProperty('serverUrl')
            def ceTaskUrl= props.getProperty('ceTaskUrl')
            def ceTask
            def analysisStatus
            while(analysisStatus != 'SUCCESS') {
                sleep(5)
                ceTask = jsonParse(new URL(ceTaskUrl).getText(requestProperties: [Authorization: "Basic " + "admin:admin".getBytes().encodeBase64().toString()]))
                analysisStatus = ceTask["task"]["status"]
            }
            def analysisId = ceTask["task"]["analysisId"]
            def analysisResultUrl = sonarServerUrl + "/api/qualitygates/project_status?analysisId=" + analysisId
            def qualitygate = jsonParse(analysisResultUrl.toURL().getText(requestProperties: [Authorization: "Basic " + "admin:admin".getBytes().encodeBase64().toString()]))
            def qualitygateStatus = qualitygate["projectStatus"]["status"]
            echo "qualitygateStatus=${qualitygateStatus}"
            if ("ERROR".equals(qualitygateStatus)) {
                error "Quality Gate failure"
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

def Properties getProperties(filename) {
    def properties = new Properties()
    properties.load(new StringReader(readFile(filename)))
    return properties
}

@NonCPS
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
