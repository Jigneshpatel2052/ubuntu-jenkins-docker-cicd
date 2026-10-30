
pipeline {
    agent any

    // Automatically check GitHub for changes approximately every 2 minutes
    triggers {
        pollSCM('H/2 * * * *')
    }

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
                    grep -qi "Alepo Technology" index.html
                    echo "Alepo website validation passed"
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
                    grep -qi "Alepo Technology" /tmp/deployed.html
                    echo "Alepo website deployment verified"
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

