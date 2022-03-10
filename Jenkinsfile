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
                sh 'mvn clean install'
            }
        }
        stage ('Deploy war file on tomcat server')
        {
            steps{
                sshagent(['tomcat-war-file']) {
                sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war centos@3.111.214.199:/opt/tomcat/webapps"
                }
            }
        }
    }
}
