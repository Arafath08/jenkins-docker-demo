pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "arafatmeeran08/jenkins-docker-demo"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/Arafath08/jenkins-docker-demo.git']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'WipeWorkspace'], [$class: 'CleanBeforeCheckout']]
                ])
                echo "✅ Checkout stage completed"
            }
        }

        stage('Test Docker Access') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
                echo "✅ Jenkins can access Docker!"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Run docker commands as root
                    sh 'docker --version'
                    sh 'docker ps'
                    sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} ."
                }
                echo "✅ Docker Image build completed"
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials',
                                                     usernameVariable: 'DOCKER_USER',
                                                     passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
                echo "✅ Docker Hub login completed"
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}"
                }
                echo "✅ Docker Image push completed"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment step goes here (Kubernetes, Ansible, Docker run, etc.)"
                echo "✅ Deploy stage completed"
            }
        }
    }
}
