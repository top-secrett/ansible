pipeline {
    agent any

    stages {
        stage('Chekout'){
            steps {
                git branch: 'main', url: "git@github.com:top-secrett/ansible.git", credentialsId: 'github-ssh-key'
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook playbook: 'playbook.yml', inventory: 'host.txt', credentialsId: 'github-ssh-key'
            }
        }
    }
    
}
