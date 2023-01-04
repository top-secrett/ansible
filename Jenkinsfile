pipeline {
    agent any

    environment {
        GIT_BRANCH = 'main'
    }

    stages {
        stage('Chekout'){
            steps {
                git branch: $GIT_BRANCH, url: "git@github.com:top-secrett/ansible.git", credentialsId: 'github-ssh-key'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ansible-playbook playbook.yml'
            }
        }
    }
    
}
