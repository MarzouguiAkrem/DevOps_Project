pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-docker-image-name'
        REGISTRY_CREDENTIALS = 'your-docker-hub-credentials-id'
        KUBE_NAMESPACE = 'your-kubernetes-namespace'
        KUBE_DEPLOYMENT_NAME = 'your-k8s-deployment-name'
        KUBE_SERVICE_NAME = 'your-k8s-service-name'
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code depuis le référentiel Git
                git branch: 'main', url: 'https://github.com/MarzouguiAKrem/DevOps_Project.git'
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                // Build de l'image Docker
                script {
                    docker.build(env.DOCKER_IMAGE)
                }

                // Connexion au registre Docker et push de l'image
                script {
                    withCredentials([usernamePassword(credentialsId: env.REGISTRY_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}"
                        sh "docker push ${env.DOCKER_IMAGE}"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Appliquer les manifestes Kubernetes
                    sh "kubectl apply -f k8s/deployment.yaml -n ${env.KUBE_NAMESPACE}"

                    // Attendre que le déploiement soit prêt
                    sh "kubectl rollout status deployment/${env.KUBE_DEPLOYMENT_NAME} -n ${env.KUBE_NAMESPACE}"

                    // Appliquer le service NodePort (pour le test local)
                    sh "kubectl apply -f k8s/service-nodeport.yaml -n ${env.KUBE_NAMESPACE}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                // Nettoyer les ressources temporaires si nécessaire
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed. Check the logs for details.'
        }
    }
}
