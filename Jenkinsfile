pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: python
    image: python:3.11
    command:
    - cat
    tty: true
"""
        }
    }

    stages {
        stage('Checkout') {
            steps {
                container('python') {
                    git branch: 'main',
                       url: 'git@github.com:jiali528/Test_project.git',
                       credentialsId: 'github-ssh-key'
                }
            }
        }

        stage('Setup') {
            steps {
                container('python') {
                    sh 'python3 -m venv venv'
                    sh '. venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Test') {
            steps {
                container('python') {
                    sh '. venv/bin/activate && pytest test_app.py'
                }
            }
        }
    }

    post {
        success {
            echo 'All tests passed!'
        }
        failure {
            echo 'Some tests failed.'
        }
    }
}

