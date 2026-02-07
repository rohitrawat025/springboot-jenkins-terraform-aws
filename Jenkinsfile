pipeline {
    agent {
        label 'docker-agent-1'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Agent Sanity Check') {
            steps {
                sh '''
                  echo "Running on Jenkins Agent"
                  hostname
                  whoami
                  pwd
                  java -version
                '''
            }
        }

    }
}

