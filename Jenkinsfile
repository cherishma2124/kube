pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    // Build and push Docker image
                    bat 'docker build -t ex:latest .'
                    bat 'docker tag ex:latest cherishma21/ex:latest'
                    bat 'docker push cherishma21/ex:latest'
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
                    // Delete and start Minikube cluster
                    bat 'minikube delete'
                    bat 'minikube start'
                    
                    // Enable the dashboard addon
                    bat 'minikube addons enable dashboard'
                    
                    // Apply Kubernetes resources
                    bat 'kubectl apply -f my-kube-deployment.yaml'
                    bat 'kubectl apply -f my-kube-service.yaml'
                    
                    // Expose the Kubernetes Dashboard service
                    bat 'minikube dashboard'
                    
                    echo 'Deploying application...'
                }
            }
        }
    }
}
