pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out GitHub repository'
                checkout scm
            }
        }

        stage('Check Ansible') {
            steps {
                sh 'ansible --version'
            }
        }

        stage('Test Connectivity') {
            steps {
                sh '''
                ansible webservers \
                -i inventory/hosts.ini \
                -m ping
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                ansible-playbook \
                -i inventory/hosts.ini \
                playbooks/deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Ansible deployment completed successfully!'
        }
        failure {
            echo 'Ansible deployment failed!'
        }
    }
}
