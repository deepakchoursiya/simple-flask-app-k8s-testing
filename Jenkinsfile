pipeline {
    agent any

    environment {
        KUBECONFIG_PATH = '/root/.kube/config'
        KUBECTL_PATH = '/tmp/kubectl'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/deepakchoursiya/simple-flask-app-k8s-testing.git'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                sh '''
                ${KUBECTL_PATH} --kubeconfig=${KUBECONFIG_PATH} apply -f k8s/deployment.yaml
                ${KUBECTL_PATH} --kubeconfig=${KUBECONFIG_PATH} apply -f k8s/service.yaml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Successfully deployed to Minikube!'
        }
        failure {
            echo '❌ Deployment to Minikube failed.'
        }
    }
}
