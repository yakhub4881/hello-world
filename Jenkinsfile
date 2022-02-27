pipeline{
    agent any
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'hello-world-ansible-git', url: 'https://github.com/yakhub4881/hello-world.git']]])
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
                 ansiblePlaybook become: true, credentialsId: 'Ansible-SSH', disableHostKeyChecking: true, installation: 'ansible2.7.5', inventory: 'dev.inv', playbook: 'master1.yml'
            }
        }
    }
}