pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    skipStagesAfterUnstable()
  }
  agent {
    kubernetes {
      inheritFrom 'c8y-hugo'
      defaultContainer 'default'
    }
  }
  environment {
    YUM_SRV = 'yum.cumulocity.com'
    YUM_USR = 'hudson'
    YUM_DEST_DIR = '/var/www/staticpage-guides/guides'
    HUGO_PARAMS = ""
  }

  stages {
    stage('Checkout') {
            steps {
                git branch: "master", credentialsId: "jenkins-master", url:'ssh://git@bitbucket.org/m2m/c8y-docs/'
            }
        }
    stage('Deploy') {
      steps {
        sshagent(['hudson-ssh-resources']) {
        sh '''bash --login
          python /docsRepoScanner.py ./
          pwd
          ls
          rsync -avh output.json ${YUM_USR}@${YUM_SRV}:${YUM_DEST_DIR}/releases.json --delete
          '''
        }
      }
    }
  }
}