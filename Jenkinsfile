pipeline
{
    agent any
    stages
    {
        stage('continuous download')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'    
            }
        }
        stage('continuous buit')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('contiuous deployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/Decpipeline/webapp/target/webapp.war ubuntu@172.31.87.185:/var/lib/tomcat9/webapps/testapp.war'
            }
        }
        stage('continous testing')
        {
            steps
          {
            git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
            
             sh 'java -jar /var/lib/jenkins/workspace/Decpipeline2/testing.jar'
          }
            
        }
    }
    post
    {
        success
        {
          sh 'scp /var/lib/jenkins/workspace/Decpipeline2/webapp/target/webapp.war  ubuntu@172.31.94.66:/var/lib/tomcat9/webapps/prodapp.war'  
        }
        failure
        {
            mail bcc: '', body: 'Jenkins has failed in CI', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'saikrishna@gmail.com'
        }
    }
    
}
