pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }


    stages {
        stage('install-pip-deps') {
            steps {
                script{
                    build()
                }
            }
        }
        stage('deploy-to-dev') {
            steps {
                script{
                    deploy("dev", 7001)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script{
                    test("dev")
                }
            }
        }
        stage('deploy-to-staging') {
            steps {
                script{
                    deploy("staging", 7002)
                }
            }
        }
        stage('tests-on-staging') {
            steps {
                script{
                    test("staging")
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script{
                    deploy("preprod", 7003)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script{
                    test("preprod")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script{
                    deploy("prod", 7004)
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script{
                    test("prod")
                }
            }
        }
    }
}

// for windows: bat "npm.."
// for linux/macos: sh "npm .."

def build(){
    echo "Installing all required depdendencies.."
    git branch: 'main', url: 'https://github.com/mtararujs/python-greetings'
    bat "dir"
    bat "pip3 install -r requirements.txt"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    git branch: 'main', url: 'https://github.com/mtararujs/python-greetings'
    bat "C:\\Users\\Max\\AppData\\Roaming\\npm\\pm2 delete greetings-app-${environment} & EXIT /B 0"
    bat "C:\\Users\\Max\\AppData\\Roaming\\npm\\pm2 start app.py --name greetings-app-${environment} -- --port ${port}"
}

def test(String environment){
    echo "Testing on ${environment} has started.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework'
    bat "dir"
    bat "npm install"
    bat "npm run greetings greetings_${environment}" 
}