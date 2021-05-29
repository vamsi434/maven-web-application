node
{
    def mavenHome = tool name:"maven3.8.1"
    stage('checkoutcode') 
    {
        git credentialsId: '02d9aa98-7fa5-472b-8994-32c12df92998',
        url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
    }
    stage('Build')
    {
     sh "${mavenHome}/bin/mvn clean package"
    }
    stage('Executesonarqubereport')
    {
     sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('Uploadartifactintonexus')
    {
     sh "${mavenHome}/bin/mvn deploy"
    }
    stage('DelpoyAppIntoTomcatServer')
    {
     sshagent(['06e24715-602d-4417-929c-cb1c7d2fd0e7']) {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.33.60:/opt/apache-tomcat-9.0.44/webapps/"
     }
    }
    stage('SendEmailNotification')
    {
     emailext body: '''Build Over-Scriptedway

      Regards,
     Mithun Software Solutions''', 
     subject: 'Build Over-Scriptedway', 
     to: 'devopstrainingblr@gmail.com'   
    }
}
