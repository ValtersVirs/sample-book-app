pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }

    stages {
        stage('Build') {
            steps {
                script {
                    build()
                }
            }
        }
        stage('Deploy on DEV') {
            steps {
                script {
                    deploy("DEV", 1010)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script {
                    test("DEV")
                }
            }
        }
        stage('Deploy on STG') {
            steps {
                script {
                    deploy("STG", 2020)
                }
            }
        }
        stage('Tests on STG') {
            steps {
                script {
                    test("STG")
                }
            }
        }
        stage('Deploy on PRD') {
            steps {
                script {
                    deploy("PRD", 3030)
                }
            }
        }
        stage('Tests on PRD') {
            steps {
                script {
                    test("PRD")
                }
            }
        }
        
    }
}

def build() {
    echo "Building of node application is starting.."
    bat "dir"
    bat "npm install"
}

def deploy(String environment, int port) {
    echo "Deployment to ${environment} has started.."
    bat "pm2 delete \"books-${environment}\""
    bat "pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String environment) {
    echo "Testing to ${environment} has started.."
}