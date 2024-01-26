pipeline {
  agent any
  tools {
    go '1.21.6'
  }
  stages {
    stage('Checkout SCM') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [
            [name: 'main']
          ],
          userRemoteConfigs: [
            [
              url: 'https://github.com/syedahmedjamil/web_app.git',
              credentialsId: '',
            ]
          ]
        ])
      }
    }
    stage('Build') {
      steps {
        echo 'Building application...'
        sh 'go build ./web_app.go'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing application....'
        sh 'pwd'
        sh 'ls -la'
        sh './web_app &'
        sh 'curl localhost:80'
        sh '''response=$(curl -s -o /dev/null -w "%{http_code}" http://localhost:80) &&
        echo Response is: $response && 
        [ "$response" = "200" ] && exit 0 || exit 1'''
      }
    }
    stage('Deploy') {
      steps {
          echo 'Deploying application...'
          sh 'date'
          sh 'id'
          sh 'sleep 1'
        // sshagent(credentials: ['creds_srv']) {
        //   sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.6.40.106 "cd web_app && git pull && go build ./web_app.go && ./web_app &"'
        // }
      }
    }
  }
}
