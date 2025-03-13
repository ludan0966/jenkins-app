pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
              docker {

               image 'node: 22.14.0-alpine'
               resuseNode true
              }
               
            }
            steps {
              sh '''
              node --version
              '''
            }
        }
    }
}
