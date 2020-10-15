node
{

  def mavenHome=tool name: "Maven"
  
 stage('Checkout')
 {
 	 git credentialsId: 'b4586e26-8c92-434c-bc26-22a3a1a15a2f', url: 'https://github.com/devopstechnologies-ec-applications/maven-web-application.git'
 
 }

 stage('Build')
 {
 sh  "${mavenHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSoanrQubeReport')
 {
 sh  "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 stage('UploadArtifactintoNexus')
 {
 sh  "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeployAppintoTomcat')
 {
sshagent(['585beb7b-8609-49bc-867b-75bc123e53b9']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.51.244:/opt/apache-tomcat-9.0.38/webapps/"
 }
 }

   /*
 stage('SendEmailNotification')
 {
 emailext body: '''Build is over..

 Regards,
 Mithun Technologies,
 9980923226.''', subject: 'Build is over', to: 'devopstrainingblr@gmail.com'
 }
 */
}
