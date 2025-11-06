pipeline {
    agent any

    options {
        skipDefaultCheckout(true) // disable Jenkins auto-checkout
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/123shran123/exp-4-devops.git'
            }
        }
        stage('Setup Environment') {
            steps {
                bat '''
                    python -m venv venv
                    call venv\\Scripts\\activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                bat '''
                    call venv\\Scripts\\activate
                    pytest --maxfail=1 --disable-warnings --junitxml=results.xml || exit 0
                '''
            }
        }
    }

    post {
        always {
            junit 'results.xml'
        }
    }
}
