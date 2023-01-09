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
                ansiblePlaybook playbook: 'playbook.yml', inventory: 'hosts.txt', credentialsId: 'github-ssh-key'
            }
        }
        
        stage('git diff'){
            steps {
                sh 'git diff $GIT_PREVIOUS_COMMIT'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: "git@github.com:top-secrett/ansible.git", credentialsId: 'github-ssh-key'
                // lastChanges since: 'LAST_SUCCESSFUL_BUILD', format:'SIDE',matching: 'LINE'
                echo "${GIT_COMMIT}"
                echo "${GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
            }
        }
        
    }    
}
