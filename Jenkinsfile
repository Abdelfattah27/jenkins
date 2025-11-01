pipeline {
    agent {
        label 'agent-0'
    }

    tools {
        maven 'mvn-3-5-2'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn package install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}