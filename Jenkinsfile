pipeline {
    agent any

    // environment{
    //     NETLIFY_SITE_ID = '8293a1d1-25f0-4b16-be49-50158afec6b4'
    //     NETLIFY_AUTH_TOKEN = credentials('myToken')
    // }
    stages {
        // stage('Docker'){
        //     steps{
        //         sh 'docker build -t my-docker-image .'
        //     }
        // }
        // stage('Build') {
        //     agent {
        //         docker {
        //             image 'node:20.11.1-alpine' 
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //         ls -la
        //         node --version
        //         npm --version
        //         npm install
        //         npm run build
        //         ls -la
        //         '''
        //     }
        // }
        //  stage('Test') {
        //     agent {
        //         docker {
        //             image 'node:20.11.1-alpine' 
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //         test -f build/index.html
        //         npm test
        //         '''
        //     }
        // }
        stage('Deploy') {
            agent {
                docker {
                    // image 'node:20.11.1-alpine' 
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-temp', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                       aws --version
                       aws s3 ls
                    '''
               }
                
            }
        }
    }
}
