pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                   url: 'git@github.com:jiali528/Test_project.git',  
                   credentialsId: 'github-ssh-key'
            }
        }

        stage('Setup') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh '. venv/bin/activate && pytest test_app.py'
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
