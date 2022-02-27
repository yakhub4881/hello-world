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
                 ansiblePlaybook become: true, credentialsId: 'Ansible-SSH', installation: 'ansible2.9.27', inventory: '/etc/ansible/master1.yml', playbook: '/etc/ansible/master1.yml'
                 sh 'ansible-playbook msater.yml'
            }
        }
    }
}