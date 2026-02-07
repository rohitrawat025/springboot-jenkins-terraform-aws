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
stage('Build with Maven') {
    steps {
        sh '''
            mvn clean package -DskipTests
        '''
    }
}
stage('Docker Build') {
    steps {
        sh '''
            docker build -t springboot-app:latest .
        '''
    }
}
stage('Terraform Init') {
    steps {
        dir('terraform') {
            sh 'terraform init'
        }
    }
}

stage('Terraform Apply') {
    steps {
        dir('terraform') {
            sh '''
                terraform apply -auto-approve \
                -var="key_name=jenkins-key"
            '''
        }
    }
}

    }
}

