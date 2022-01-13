node('master')
{
    stage('ContinuousDownload') 
    {
         git 'https://github.com/venkat9822891/mymaven.git'
    }
    stage('ContinuousBuild') 
    {
         sh label: '', script: 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.45.221:/var/lib/tomcat9/webapps/testenv.war'
    }
    stage('ContinuousTesting')
    {
        git 'https://github.com/venkat9822891/Selenium-testcases.git'
        sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
     stage('ContinuousDelivery')
    {
        input message: 'Waiting for Approval from the DM', submitter: 'Srinivas'
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.13.130:/var/lib/tomcat9/webapps/prodenv.war'
    }
    
    
}
