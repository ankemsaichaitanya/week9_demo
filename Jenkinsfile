pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    bat 'docker login -u ankemchaitu -p ankem@2411'
                    bat 'docker build -t w9-dd-app:latest .'
                    bat 'docker tag w9-dd-app:latest ankemchaitu/week9_demo:latest'
                    bat 'docker push ankemchaitu/week9_demo:latest'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // ❌ removed delete to avoid long wait
                    bat 'minikube start --driver=docker --wait=true'

                    bat 'minikube addons enable dashboard'
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'

                    echo 'Deploying application...'
                    bat 'minikube service list'
                }
            }
        }
    }
}
