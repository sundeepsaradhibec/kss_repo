
pipeline {
    agent any

    stages {
        stage('Checkout Source Code') {
            steps {
                checkout scm
                echo 'Source code downloaded from Git.'
            }
        }

        stage('Check Tools') {
            steps {
                sh 'java -version'
                sh 'docker --version'
                sh 'ansible-playbook --version'
            }
        }

        stage('Build and Deploy using Ansible') {
            steps {
                sh 'ansible-playbook -i localhost, deploy.yml'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps -a --filter name=java-demo'
                sh 'docker logs java-demo'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the Jenkins console output.'
        }
    }
}
