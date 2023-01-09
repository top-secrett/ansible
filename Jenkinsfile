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
                lastChanges since: 'LAST_SUCCESSFUL_BUILD', format:'SIDE',matching: 'LINE'
            }
        }
        
        stage("last-changes") {
        def publisher = LastChanges.getLastChangesPublisher "PREVIOUS_REVISION", "SIDE", "LINE", true, true, "", "", "", "", ""
              publisher.publishLastChanges()
              def changes = publisher.getLastChanges()
              println(changes.getEscapedDiff())
              for (commit in changes.getCommits()) {
                  println(commit)
                  def commitInfo = commit.getCommitInfo()
                  println(commitInfo)
                  println(commitInfo.getCommitMessage())
                  println(commit.getChanges())
              }
        }
    }    
}
