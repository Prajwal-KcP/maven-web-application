node{
    
echo "Jenkins home dir is: ${env.JENKINS_HOME}"
echo "Job name is: ${env.JOB_NAME}"
echo "Build number is: ${env.BUILD_NUMBER}"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false], [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

def mavenHome = tool name: 'maven3.9.3'

stage('CheckOutCode'){
git branch: 'development', credentialsId: 'edc4b3c1-e793-439e-a146-0b13821b5050', url: 'https://github.com/Prajwal-KcP/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactsIntoNexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['72d63ce7-824b-4ba0-91fa-75ec6c2f799a']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.15.23:/opt/apache-tomcat-9.0.76/webapps/"
}
}
*/

}
