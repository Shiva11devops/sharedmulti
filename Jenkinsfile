pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/Shiva11devops/maven10.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               sh 'scp /var/lib/jenkins/workspace/job1/webapp/target/webapp.war ubuntu@172.31.32.29:/var/lib/tomcat9/webapps/webapp2/testapp.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/Shiva11devops/testing1.git'
               sh 'java -jar /var/lib/jenkins/workspace/job1/testing.jar'
            }
        }
       
    }
    
    post
    {
        success
        {
            input message: 'Need approval from the DM!', submitter: 'approval'
               sh 'scp /var/lib/jenkins/workspace/job1/webapp/target/webapp.war ubuntu@172.31.44.139:/var/lib/tomcat9/webapps/webapp2/prodapp.war'
        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'shivasai100@gmail.com'
        }
       
    }
    
    
    
    
    
    
}
