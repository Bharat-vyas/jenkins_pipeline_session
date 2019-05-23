node {
      stage('Scm Checkout'){
      git credentialsId: '70879577-c865-415b-b4cb-0c6e86882477', url: 'https://www.github.com/Bharat-vyas/jenkins_pipeline_session.git'
}
 
/*	
if (env.BRANCH_NAME == 'master')
{

    stage ('Build Web Image')
    {
    sh "docker build -t bharatvyas/jenkins_demo:${env.BUILD_ID} -f docker/Dockerfile ."
    }

     stage('Push image to dockerhub'){
	withDockerRegistry(credentialsId: '996ea76f-df01-4824-9db3-0bc3a7c24c21'){
	sh 'docker push bharatvyas/jenkins_demo'
     }
/*
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
}*/
//}


//} //node close

/*
def Properties getProperties(filename) {
    def properties = new Properties()
    properties.load(new StringReader(readFile(filename)))
    return properties
}

@NonCPS
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
