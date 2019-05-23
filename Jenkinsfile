node {

// Defining Variables
def webPath = '/home/docker/DrinkSavvy/web/portal'
def dockerRegistry='dockerregistry.ecosmob.net:5000'

	stage ('Checkout'){
	    checkout scm
    	}




 if (env.BRANCH_NAME == 'release')
{
withCredentials( [usernamePassword( credentialsId: 'kishortest', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
{
  def remote = [:]
  remote.name = 'digitalocean'
  remote.host = '206.189.132.253'
  remote.user = "${USERNAME}"
  remote.password = "${PASSWORD}"
  remote.allowAnyHosts = true
/*  stage('DB deployment') 
  {
   sshPut remote: remote, from: './docker/db/docker-compose.yml', into: "${dbPath}"
   sshCommand remote: remote, command: "mkdir -p $dbPath ; docker-compose -f $dbPath/docker-compose.yml down; sleep 5 ; docker-compose -f $dbPath/docker-compose.yml up -d ; docker ps "
  }
*/
    stage ('Build Web Image')
    {
    sh "docker build -t ${dockerRegistry}/drinksavvy-portal:v1 -f docker/web/Dockerfile ."
    }
  
    stage ('Docker Push Web Image')
    {
    sh "docker login -u=ecosmob -p=$PASSWORD ${dockerRegistry} ; docker push ${dockerRegistry}/drinksavvy-portal:v1 ;docker logout ${dockerRegistry}"
    } 
}

withCredentials( [usernamePassword( credentialsId: 'kishortest', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
{
  def remote = [:]
  remote.name = 'VM'
  remote.host = '206.189.132.253'
  remote.user = "${USERNAME}"
  remote.password = "${PASSWORD}"
  remote.allowAnyHosts = true
  stage('Pull and Deploy Web Image') 
  {
    sshCommand remote: remote, command: "docker login -u=ecosmob -p=$PASSWORD ${dockerRegistry} ; docker pull ${dockerRegistry}/drinksavvy-portal:v1 ;docker logout ${dockerRegistry}; docker images ; mkdir -p ${webPath} "
    sshPut remote: remote, from: './docker/web/nginx.conf', into: "${webPath}"
    sshPut remote: remote, from: './docker/web/www.conf', into: "${webPath}"
    sshPut remote: remote, from: './docker/web/php.ini', into: "${webPath}"
    sshPut remote: remote, from: './docker/web/docker-compose.yml', into: "${webPath}"
    sshCommand remote: remote, command: "docker-compose -f $webPath/docker-compose.yml down; sleep 5; docker-compose -f $webPath/docker-compose.yml up -d ; docker ps"
  }
}
}


} node close


def Properties getProperties(filename) {
    def properties = new Properties()
    properties.load(new StringReader(readFile(filename)))
    return properties
}

@NonCPS
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
