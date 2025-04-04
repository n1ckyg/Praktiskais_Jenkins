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
    
        stage('deploy-to-dev'){
            steps{
                script{
                    deploy("dev", 7001)
                }
            }
        }
    
        stage('tests-on-dev'){
            steps{
                echo "Testing dev..."
            }
        }

        stage('deploy-to-staging'){
            steps{
                script{
                    deploy("staging", 7002)
                }
            }
        }

        stage('tests-on-staging'){
            steps{
                echo "Testing staging..."
            }
        }

        stage('deploy-to-preprod'){
            steps{
                script{
                    deploy("preprod", 7003)
                }
            }
        }

        stage('tests-on-preprod'){
            steps{
                echo "Testing preprod..."
            }
        }

        stage('deploy-to-prod'){
            steps{
                script{
                    deploy("prod", 7004)
                }
            }
        }

        stage('tests-on-prod'){
            steps{
                echo "Testing prod..."
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
    bat "npm install pm2"
    echo "Checking folder for necessary files...."
    bat "dir"
    echo "Delete existing pm2 processes.."
    bat "pm2 delete greetings-app-${environment} & EXIT /B 0"
    echo "Launching pm2 processes.."
    bat "pm2 start app.py --name greetings-app-${environment} --port ${port}"
}