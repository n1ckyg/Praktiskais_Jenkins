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
                echo "Deploying to dev"
            }
        }
    
        stage('tests-on-dev'){
            steps{
                echo "Testing dev..."
            }
        }

        stage('deploy-to-staging'){
            steps{
                echo "Deploying to staging..."
            }
        }

        stage('tests-on-staging'){
            steps{
                echo "Testing staging..."
            }
        }

        stage('deploy-to-preprod'){
            steps{
                echo "Deploying to preprod..."
            }
        }

        stage('tests-on-preprod'){
            steps{
                echo "Testing preprod..."
            }
        }

        stage('deploy-to-prod'){
            steps{
                echo "Deploying to prod..."
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
    echo "Cloning repository"
    git branch: 'main', poll: false, url: 'https://github.com/n1ckyg/python-greetings.git'
    echo "Checking folder fol necessary files...."
    bat "dir"
}