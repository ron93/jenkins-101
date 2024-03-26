pipeline {
    agent any
    // agent { 
    //     node {
    //         label 'docker_agent_python'
    //         }
    //   }
      triggers {
        pollSCM '* * * * *'
      }
    stages { 
        stage('checkout') {
            steps {
                git(url: 'https://github.com/ron93/jenkins-101.git', branch:'master')
            }
        }
        stage('list') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt

                '''
            }
        }
        stage('Test') {
            parallel {
                stage('Test app') {
                steps {
                    echo "Testing.."
                    sh '''
                    cd myapp
                    python3 hello.py
                    python3 hello.py --name=Ron
                    '''
                }}
                stage("Test cli") {
                    steps {
                        echo "Testin parallel ..."
                    }
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}