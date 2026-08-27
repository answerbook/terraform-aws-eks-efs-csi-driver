def CREDS = [
    string(credentialsId: 'github-api-token',
           variable: 'GITHUB_TOKEN')
]

pipeline {
  agent {
    node {
      label 'ec2-fleet'
    }
  }

  options {
    timeout time: 1, unit: 'HOURS'
    timestamps()
    ansiColor 'xterm'
    withCredentials(CREDS)
  }

  stages {

    stage('Publish') {
      when {
        anyOf {
          branch "master"
          branch "main"
        }
      }
      steps {
        sh '''echo "Create and push tag to GitHub repo"
              git fetch
              git tag $(svu next --force-patch-increment)
              git push --tags
            '''
      }
    }
  }
}
