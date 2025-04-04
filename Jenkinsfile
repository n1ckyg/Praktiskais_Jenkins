pipeline {
    agent any
    //triggers{ pollSCM('*/1 * * * *') }

    stages {
        stage('install-pip-deps'){
            steps{
                script{
                    python_dependencies()
                }
            }
        }
    
        stage("deploy-to-dev"){
            steps{
                script{
                    deploy("dev", 7001)
                }
            }
        }
    
        stage('tests-on-dev'){
            steps{
                script{
                    test("dev")
                }
            }
        }

        stage("deploy-to-staging"){
            steps{
                script{
                    deploy("staging", 7002)
                }
            }
        }

        stage('tests-on-staging'){
            steps{
                script{
                    test("staging")
                }
            }
        }

        stage("deploy-to-preprod"){
            steps{
                script{
                    deploy("preprod", 7003)
                }
            }
        }

        stage('tests-on-preprod'){
            steps{
                script{
                    test("preprod")
                }
            }
        }

        stage("deploy-to-prod"){
            steps{
                script{
                    deploy("prod", 7004)
                }
            }
        }

        stage('tests-on-prod'){
            steps{
               script{
                    test("prod")
                }
            }
        }
    }
}       

def python_dependencies (){
    echo "Cloning python-greetings repository"
    git branch: 'main', poll: false, url: 'https://github.com/n1ckyg/python-greetings.git'
    echo "Checking folder for necessary files...."
    bat "dir"
    echo "Installing Python"
    bat "pip install -r requirements.txt"
}

def deploy (String environment, int port){
    echo "Cloning python-greetings repository"
    git branch: 'main', poll: false, url: 'https://github.com/n1ckyg/python-greetings.git'
    echo "Installing NPM"
    bat "npm install"
    echo "Checking folder for necessary files...."
    bat "dir"
    echo "Delete existing pm2 processes.."
    bat "node_modules\\.bin\\pm2 delete greetings-app-${environment} & EXIT /B 0"
    echo "Launching pm2 processes.."
    bat "node_modules\\.bin\\pm2 start app.py --name greetings-app-${environment} -- --port ${port}"
    bat "node_modules\\.bin\\pm2 list"
}

def test (String environment){
    echo "Cloning python-greetings repository"
    git branch: 'main', poll: false, url: 'https://github.com/n1ckyg/course-js-api-framework.git'
    echo "Installing NPM"
    bat "npm install"
    echo "Checking folder for necessary files...."
    bat "dir"
    echo "Running tests for ${environment} environment"
    bat "npm run greetings greetings_${environment}"
}

//bat "node_modules\\.bin\\pm2 delete \"books-${environment}\" || exit 0"
//bat "node_modules\\.bin\\pm2 start -n \"books-${environment}\" index.js -- ${port}"
