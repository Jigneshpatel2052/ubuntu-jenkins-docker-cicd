
pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                sh '''
                    set -eu
                    test -s index.html
                    grep -q "Deployment successful!" index.html
                    echo "HTML validation passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -eu
                    install -m 0644 index.html /opt/devops-site/index.html
                '''
            }
        }

        stage('Smoke Test') {
            steps {
                sh '''
                    set -eu
                    curl --fail --silent --show-error \
                      http://127.0.0.1:8081/ -o /tmp/deployed.html
                    grep -q "Deployment successful!" /tmp/deployed.html
                    echo "Deployment verification passed"
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
