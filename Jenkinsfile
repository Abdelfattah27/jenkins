@Library('java')_

pipeline {
    agent {
        label 'agent-0'
    }

    tools {
        maven 'mvn-3-5-2'
    }

    environment {
        dockerUserName = credentials("docker-user")
        dockerPassword = credentials("docker-pass")
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
                    buildfun.build("man218/java-repo", "${BUILD_NUMBER}")
                }
            }
        }
        stage('Docker push') {
            steps {
                script {
                    def buildfun = new edu.iti.docker()
                    buildfun.login("${dockerUserName}", "${dockerPassword}")
                    buildfun.push("man218/java-repo", "${BUILD_NUMBER}")
                }
            }
        }
    }
}