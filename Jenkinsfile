node()
{
def maven_home = tool name : "maven3.6.0"
stage('checkoutCodeGithub')
{
git branch: 'development', credentialsId: 'd283cd7c-8625-447f-9be6-cf9a11847147', url: 'https://github.com/mithun-divya/maven-web-application.git'
}
stage('Build')
{
sh "${maven_home}/bin/mvn clean package"
}
stage('Sonar Report')
{
sh "${maven_home}/bin/mvn clean sonar:sonar"
}
stage('Nexus Repository')
{
sh "${maven_home}/bin/mvn clean deploy"
}
stage('Deploy To tomcat')
{
sshagent(['022222bb-fb44-4549-8b9a-e95c50aeca77']){
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.215.123:/opt/apache-tomcat-9.0.73/webapps"
}
}
/*
stage('send Email')
{
mail bcc: 'divya.vegesna55@gmail.com', body: '''Hi,
Build completed.
Regards,
Divya''', cc: 'divya.vegesna55@gmail.com', from: '', replyTo: '', subject: 'Build', to: 'divya.vegesna55@gmail.com'
}
*/

}

