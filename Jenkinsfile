node{


//echo "GitHub BranhName ${env.BRANCH_NAME}"
  //echo "Jenkins Job Number ${env.BUILD_NUMBER}"
  echo "Jenkins Node Name ${env.NODE_NAME}"
 */ 
  echo "Jenkins Home ${env.JENKINS_HOME}"
  echo "Jenkins URL ${env.JENKINS_URL}"
  echo "JOB Name ${env.JOB_NAME}"
  */
  
def mavenHome = tool name: "maven3.8.3"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

stage('CheckOutCode'){
git credentialsId: 'd70ace23-962a-4614-8d36-0351dfdb31ce', url: 'https://github.com/LK-apps/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('ExecuteSOnarQubeReport'){
sh "mvn  sonar:sonar"
}

stage('UploadArtifactsIntoNexusRepo'){
sh "mvn deploy"
}
*/
stage('DeployAppintoTomcatServer'){
 sshagent(['e12a3ed8-ec52-46f6-beb3-446f81bd6ba5']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.186.179:/opt/apache-tomcat-9.0.62/webapps/"     
}
}
/*
stage('SendEmailNotification'){

mail bcc: '', body: '''Build Over..

Regards,
Mithun Software Solutions,
9980923226''', cc: 'devopstrainingblr@gmail.com', from: '', replyTo: '', subject: 'Build over!...', to: 'devopstrainingblr@gmail.com'
}
*/

}
