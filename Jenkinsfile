pipeline{
    agent any
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/hello-world.git']]])
            }
        }
        stage ('BUILD')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ('Deploy war file on Tomcat Server')
        {
            steps{
                 sshagent(['Tomcat-SSH']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war centos@65.1.1.72:/opt/tomcat/webapps"
                 }
            }
        }
    }
}