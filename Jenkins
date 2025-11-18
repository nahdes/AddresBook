pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    options {
        buildDiscarder logRotator(
            daysToKeepStr: '30',
            numToKeepStr: '1'
        )
    }

    environment {
        DOCKERHUB_CRED = credentials('1')  
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/nahdes/AddresBook.git'
                    ]]
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t nahdes/address-book:${BUILD_NUMBER} ."
            }
        }

        stage('DockerHub Push') {
            steps {
                sh "echo $DOCKERHUB_CRED_PSW | docker login -u $DOCKERHUB_CRED_USR --password-stdin"
                sh "docker push nahdes/address-book:${BUILD_NUMBER}"
            }
        }

        stage('Docker Run') {
            steps {
                sh "docker rm -f addressbook || true"
                sh "docker run -d -p 4000:8080 --name addressbook nahdes/address-book:${BUILD_NUMBER}"
            }
        }
    }

    post {
        always {
            echo 'Job is completed'
        }
        success {
            echo 'It is a success'
        }
        failure {
            echo 'It has failed'
        }
    }
}