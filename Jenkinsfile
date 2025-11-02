@Library('java')_

pipeline {
    agent {
        label 'agent-0'
    }

    tools {
        maven 'mvn-3-5-2'
    }

    environment {
        dockerPassword = credentials("dockerhub-pass")
    }

    stages {
        stage('Build') {
            steps {
                script {
                    def mavenfun = new edu.iti.maven()
                    mavenfun.mvn("package install")
                }
                
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    def buildfun = new edu.iti.docker()
                    buildfun.build("abdelfattah273/jenkinslab", "${BUILD_NUMBER}")
                }
            }
        }
        stage('Docker push') {
            steps {
                script {
                    def buildfun = new edu.iti.docker()
                    buildfun.login("abdelfattah273", "${dockerPassword}")
                    buildfun.push("abdelfattah273/jenkinslab", "${BUILD_NUMBER}")
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                script {
                    def deployfun = new edu.iti.docker()
                    deployfun.deploy("abdelfattah273/jenkinslab", "${BUILD_NUMBER}")
                }
            }
        }
    }
    post {
        always {
            cleanWs()    
        success {
            echo 'success'
        }
        failure {
            echo 'failed'
        }
    }
}
}