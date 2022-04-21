pipeline
{
    agent any
    stages
    {
        stage('Continuous Build')
        {
            steps
            {
                git 'https://github.com/pratiksponde/Jenkins-Ansible.git'
            }
        }
        stage('Execute Ansible')
        {
            steps
            {
                ansiblePlaybook credentialsId: 'Deployment-server', disableHostKeyChecking: true, installation: 'ansible', inventory: 'dev.inv', playbook: 'apache.yml'
            }
        }
    }
}
