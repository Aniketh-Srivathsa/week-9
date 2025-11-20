pipeline {
    agent any 

    stages {

        stage('Build') {
            steps {
                script {
                    // Login to DockerHub
                    bat 'docker login -u VAnikethSrivathsa -p igotdumped5694'

                    // Build image
                    bat 'docker build -t w9-dd-app:latest .'

                    // Tag image for DockerHub (repo name must be lowercase)
                    bat 'docker tag w9-dd-app:latest anikethsrivathsa/w9-dh-app:latest'

                    // Push image
                    bat 'docker push anikethsrivathsa/w9-dh-app:latest'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Fresh Minikube start
                    bat 'minikube delete'
                    bat 'minikube start'

                    // Enable dashboard addon
                    bat 'minikube addons enable dashboard'

                    // Apply K8s manifests
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'

                    // Print Dashboard URL instead of opening browser
                    bat 'minikube dashboard --url'

                    echo 'Deploying application...'
                }
            }
        }
    }
}
