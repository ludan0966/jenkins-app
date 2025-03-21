pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = '8293a1d1-25f0-4b16-be49-50158afec6b4'
        NETLIFY_AUTH_TOKEN = credentials('myToken')
    }
    stages {
        stage('Docker'){
            steps{
                sh 'docker build -t my-docker-image .'
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:20.11.1-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm install
                npm run build
                ls -la
                '''
            }
        }
         stage('Test') {
            agent {
                docker {
                    image 'node:20.11.1-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    // image 'node:20.11.1-alpine' 
                    image 'my-docker-image'
                    reuseNode true
                }
            }
            steps {
                sh '''
                # npm install netlify-cli
                # node_modules/.bin/netlify --version
                # echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                # node_modules/.bin/netlify status
                # node_modules/.bin/netlify deploy --prod --dir=build

                #####custom docker image
                netlify --version
                echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                netlify status
                netlify deploy --prod --dir=build
                '''
            }
        }
    }
}
